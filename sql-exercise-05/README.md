```python
from datetime import datetime

from sqlalchemy import (MetaData, Table, Column, Integer, Numeric, String, DateTime, 
                        ForeignKey, Boolean, create_engine, CheckConstraint)

metadata = MetaData()

cookies = Table('cookies', metadata, 
               Column('cookie_id', Integer(), primary_key=True),
               Column('cookie_name', String(50), index=True),
               Column('cookie_recipe_url', String(255)),
               Column('cookie_sku', String(55)),
               Column('quantity', Integer()),
               Column('unit_cost', Numeric(12, 2)),
               CheckConstraint('quantity > 0', name='quantity_positive')
               )

users = Table('users', metadata,
    Column('user_id', Integer(), primary_key=True),
    Column('username', String(15), nullable=False, unique=True ),
    Column('email_address', String(255), nullable=False),
    Column('phone', String(20), nullable=False),
    Column('password', String(25), nullable=False),
    Column('created_on' , DateTime(), default=datetime.now),
    Column('updated_on' , DateTime(), default=datetime.now, onupdate=datetime.now)            
)

orders = Table('orders', metadata,
    Column('order_id' , Integer()),
    Column('user_id', ForeignKey('users.user_id')),
    Column('shipped', Boolean(), default=False)
)
            
line_items = Table('line_items', metadata,
    Column('line_items_id', Integer(), primary_key=True),
    Column('order_id', ForeignKey('orders.order_id')),
    Column('cookie_id', ForeignKey('cookies.cookie_id')),
    Column('quantity', Integer()),
    Column('extended_cost', Numeric( 12, 2))
)

engine = create_engine('sqlite:///:memory:')
metadata.create_all(engine)
connection = engine.connect()
```


```python
from sqlalchemy import select, insert, update
ins = insert(users).values(
    username="cookiemon",
    email_address="mon@cookie.com",
    phone="111-111-1111",
    password="password"
)
result = connection.execute(ins)
```


```python
ins = cookies.insert()
inventory_list = [
    {
        'cookie_name': 'chocolate chip',
        'cookie_recipe_url': 'http://some.aweso.me/cookie/recipe.html',
        'cookie_sku': 'CC01',
        'quantity': '12',
        'unit_cost': '0.50'
    },
    {
        'cookie_name': 'dark chocolate chip',
        'cookie_recipe_url': 'http://some.aweso.me/cookie/recipe_dark.html',
        'cookie_sku': 'CC02',
        'quantity': '1',
        'unit_cost': '0.75'
    }
]
result = connection.execute(ins, inventory_list)
```


```python
ins = insert(orders).values(user_id=1, order_id=1)
result = connection.execute(ins)
ins = insert(line_items)
order_items = [
    {
        'order_id': 1,
        'cookie_id': 1,
        'quantity': 9,
        'extended_cost': 4.50
    }
]
result = connection.execute(ins, order_items)
```


```python
ins = insert(orders).values(user_id=1, order_id=2)
result = connection.execute(ins)
ins = insert(line_items)
order_items = [
    {
        'order_id': 2,
        'cookie_id': 2,
        'quantity': 1,
        'extended_cost': 1.50
    },
    {
        'order_id': 2,
        'cookie_id': 1,
        'quantity': 4,
        'extended_cost': 4.50
    }
]
result = connection.execute(ins, order_items)
```


```python
def ship_it(order_id):
    
    s = select([line_items.c.cookie_id, line_items.c.quantity])
    s = s.where(line_items.c.order_id == order_id)
    cookies_to_ship = connection.execute(s)
    
    for cookie in cookies_to_ship:
        u = update(cookies).where(cookies.c.cookie_id == cookie.cookie_id)
        u = u.values(quantity = cookies.c.quantity -cookie.quantity)
        result = connection.execute(u)
    
    u = update(orders).where(orders.c.order_id == order_id)
    u = u.values(shipped=True)
    result = connection.execute(u)
    print("Shipped order ID: {}".format(order_id))
```


```python
ship_it(1)
```

    Shipped order ID: 1
    


```python
s = select([cookies.c.cookie_name, cookies.c.quantity])
connection.execute(s).fetchall()
```




    [('chocolate chip', 3), ('dark chocolate chip', 1)]




```python
u = update(cookies).where(cookies.c.cookie_name == "dark chocolate chip")
u = u.values(quantity = 1)
result = connection.execute(u)
```


```python
from sqlalchemy.exc import IntegrityError
def ship_it(order_id):
    s = select([line_items.c.cookie_id, line_items.c.quantity])
    s = s.where(line_items.c.order_id == order_id)
    transaction = connection.begin()
    cookies_to_ship = connection.execute(s).fetchall()
    try:
        for cookie in cookies_to_ship:
            u = update(cookies).where(cookies.c.cookie_id == cookie.cookie_id)
            u = u.values(quantity = cookies.c.quantity-cookie.quantity)
            result = connection.execute(u)
        u = update(orders).where(orders.c.order_id == order_id)
        u = u.values(shipped=True)
        result = connection.execute(u)
        print("Shipped order ID: {}".format(order_id))
        transaction.commit()
        
    except IntegrityError as error:
        transaction.rollback()
        print(error)
```


```python
ship_it(2)
```

    (sqlite3.IntegrityError) CHECK constraint failed: quantity_positive
    [SQL: UPDATE cookies SET quantity=(cookies.quantity - ?) WHERE cookies.cookie_id = ?]
    [parameters: (1, 2)]
    (Background on this error at: http://sqlalche.me/e/13/gkpj)
    


```python
s = select([cookies.c.cookie_name, cookies.c.quantity])
connection.execute(s).fetchall()
```




    [('chocolate chip', 3), ('dark chocolate chip', 1)]




```python
# Without using a database, there are several ways data could be stored depending on the lifespan and 
# accessibility required. The simplest way to store data would simply be in memory. Using this method, 
# the data would only be accessible to the user during a session, and would not be persistent, nor shareable. 
# A simple calculator program for example, would most likely not suffer any drawbacks using this method.  
# Another way to store data would be using an external file. Depending on the use case, this could be a simple 
# text file that stores preferences, or an entirely local full-fledged database. Using this method, data could 
# persist between sessions. Sharing data between two separate users however, would be difficult.
```

## Jonathan Doolittle


```python

```
