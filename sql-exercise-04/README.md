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
from sqlalchemy import select, insert
ins = insert(users).values(
    username="cookiemon",
    email_address="mon@cookie.com",
    phone="111-111-1111",
    password="password"
)
result = connection.execute(ins)
```


```python
s = select([users.c.username])
results = connection.execute(s)
for result in results:
    print(result.username)
```

    cookiemon
    


```python
from sqlalchemy.exc import IntegrityError

ins = insert(users).values(
    username="cookiemon",
    email_address="damon@cookie.com",
    phone="111-111-1111",
    password="password"
)
try:
    result = connection.execute(ins)
except IntegrityError as error:
    print(error)
```

    (sqlite3.IntegrityError) UNIQUE constraint failed: users.username
    [SQL: INSERT INTO users (username, email_address, phone, password, created_on, updated_on) VALUES (?, ?, ?, ?, ?, ?)]
    [parameters: ('cookiemon', 'damon@cookie.com', '111-111-1111', 'password', '2022-04-13 16:07:26.861495', '2022-04-13 16:07:26.861495')]
    (Background on this error at: http://sqlalche.me/e/13/gkpj)
    


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
    },
        {
        'cookie_name': 'peanut butter',
        'cookie_recipe_url': 'http://some.aweso.me/cookie/peanut.html',
        'cookie_sku': 'PB01',
        'quantity': '24',
        'unit_cost': '0.25'
    },
        {
        'cookie_name': 'oatmeal raisin',
        'cookie_recipe_url': 'http://some.aweso.me/cookie/raisin.html',
        'cookie_sku': 'EWW01',
        'quantity': '100',
        'unit_cost': '1.00'
    }
]
result = connection.execute(ins, inventory_list)
```


```python
result.rowcount
```




    4




```python
# sing this new information regarding Python and SQL, I can see a number of potential use cases. From a data mining 
# perspective, I could see this being a valuable link between a program and a data source. For example, imagine a program 
# designed to generate insights about a particular type of data (Say, metrics regarding the price of cars). Using our 
# SQL knowledge, we could build an intermediate program that pulls data from different regions, and then puts this data 
# in a format the primary program could read. This would allow further knowledge creation of correlations between regions. 
# Outside of data science, I know there exist many libraries for game development using Python. I could see this being 
# useful for interacting with other players, such as sharing high scores or having a global leaderboard. 
```

## Jonathan Doolittle


```python

```
