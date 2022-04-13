```python
from datetime import datetime
from sqlalchemy import (MetaData, Table, Column, Integer, Numeric, String, DateTime, ForeignKey, Boolean, create_engine)

metadata = MetaData()

cookies = Table('cookies', metadata, 
                Column('cookie_id', Integer(), primary_key=True),
                Column('cookie_name', String(50), index=True),
                Column('cookie_recipe_url', String(255)),
                Column('cookie_sku', String(55)),
                Column('quantity', Integer()),
                Column('unit_cost', Numeric(12, 2)))

users = Table('users', metadata, 
                Column('user_id', Integer(), primary_key=True),
                Column('customer_number', Integer(), autoincrement=True),
                Column('username', String(15), nullable=False, unique=True),
                Column('email_address', String(255), nullable=False),
                Column('phone', String(20), nullable=False),
                Column('password', String(25), nullable=False),
                Column('created_on', DateTime(), default=datetime.now),
                Column('updated_on', DateTime(), default=datetime.now, onupdate=datetime.now))

orders = Table('orders', metadata, 
                Column('order_id', Integer(), primary_key=True),
                Column('user_id', ForeignKey('users.user_id')),
                Column('shipped', Boolean(), default=False))

line_items = Table('line_items', metadata, 
                Column('line_items_id', Integer(), primary_key=True),
                Column('order_id', ForeignKey('orders.order_id')),
                Column('cookie_id', ForeignKey('cookies.cookie_id')),
                Column('quantity', Integer()),
                Column('extended_cost', Numeric(12, 2)))

engine = create_engine('sqlite:///:memory:')
metadata.create_all(engine)
```


```python
connection = engine.connect()
```


```python
ins = cookies.insert().values(cookie_name="chocolate chip", cookie_recipe_url="http://some.aweso.me/cookie/recipe.html", cookie_sku="CC01", quantity="12", unit_cost="0.50")
print(str(ins))
```

    INSERT INTO cookies (cookie_name, cookie_recipe_url, cookie_sku, quantity, unit_cost) VALUES (:cookie_name, :cookie_recipe_url, :cookie_sku, :quantity, :unit_cost)
    


```python
ins.compile().params
```




    {'cookie_name': 'chocolate chip',
     'cookie_recipe_url': 'http://some.aweso.me/cookie/recipe.html',
     'cookie_sku': 'CC01',
     'quantity': '12',
     'unit_cost': '0.50'}




```python
result = connection.execute(ins)
result.inserted_primary_key
```




    [1]




```python
from sqlalchemy import insert
ins = insert(cookies).values(cookie_name="chocolate chip", 
                             cookie_recipe_url="http://some.aweso.me/cookie/recipe.html", 
                             cookie_sku="CC01", 
                             quantity="12", 
                             unit_cost="0.50")
str(ins)
```




    'INSERT INTO cookies (cookie_name, cookie_recipe_url, cookie_sku, quantity, unit_cost) VALUES (:cookie_name, :cookie_recipe_url, :cookie_sku, :quantity, :unit_cost)'




```python
ins = cookies.insert()
result = connection.execute(ins, 
                            cookie_name="dark chocolate chip", 
                            cookie_recipe_url="http://some.aweso.me/cookie/recipe_dark.html", 
                            cookie_sku="CC02", 
                            quantity="1", 
                            unit_cost="0.75")
```


```python
result.inserted_primary_key
```




    [2]




```python
inventory_list = [
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
```


```python
result = connection.execute(ins, inventory_list)
```


```python
from sqlalchemy.sql import select
```


```python
s = select([cookies])
```


```python
str(s)
```




    'SELECT cookies.cookie_id, cookies.cookie_name, cookies.cookie_recipe_url, cookies.cookie_sku, cookies.quantity, cookies.unit_cost \nFROM cookies'




```python
rp = connection.execute(s)
```


```python
results = rp.fetchall()
```


```python
first_row = results[0]
first_row[1]
```




    'chocolate chip'




```python
s = cookies.select()
```


```python
rp = connection.execute(s)
```


```python
for record in rp:
    print(record.cookie_name)
```

    chocolate chip
    dark chocolate chip
    peanut butter
    oatmeal raisin
    


```python
s = select([cookies.c.cookie_name, cookies.c.quantity])
rp = connection.execute(s)
print(rp.keys())
results = rp.fetchall()
```

    ['cookie_name', 'quantity']
    


```python
results
```




    [('chocolate chip', 12),
     ('dark chocolate chip', 1),
     ('peanut butter', 24),
     ('oatmeal raisin', 100)]




```python
s = select([cookies.c.cookie_name, cookies.c.quantity])
s = s.order_by(cookies.c.quantity, cookies.c.cookie_name)
rp = connection.execute(s)
for cookie in rp:
    print('{} - {}'.format(cookie.quantity, cookie.cookie_name))
```

    1 - dark chocolate chip
    12 - chocolate chip
    24 - peanut butter
    100 - oatmeal raisin
    


```python
s = select([cookies.c.cookie_name, cookies.c.quantity])
s = s.order_by(cookies.c.quantity)
s = s.limit(2)
rp = connection.execute(s)
print([result.cookie_name for result in rp])
```

    ['dark chocolate chip', 'chocolate chip']
    


```python
from sqlalchemy.sql import func
```


```python
s = select([func.count(cookies.c.cookie_name)])
rp = connection.execute(s)
record = rp.first()
print(record.keys())
print(record.count_1)
```

    ['count_1']
    4
    


```python
s = select([func.count(cookies.c.cookie_name).label('inventory_count')])
rp = connection.execute(s)
record = rp.first()
print(record.keys())
print(record.inventory_count)
```

    ['inventory_count']
    4
    


```python
s = select([cookies]).where(cookies.c.cookie_name == 'chocolate chip')
rp = connection.execute(s)
record = rp.first()
print(record.items())
```

    [('cookie_id', 1), ('cookie_name', 'chocolate chip'), ('cookie_recipe_url', 'http://some.aweso.me/cookie/recipe.html'), ('cookie_sku', 'CC01'), ('quantity', 12), ('unit_cost', Decimal('0.50'))]
    


```python
s = select([cookies]).where(cookies.c.cookie_name.like('%chocolate%')).where(cookies.c.quantity == 12)
rp = connection.execute(s)
for record in rp.fetchall():
    print(record.cookie_name)
```

    chocolate chip
    


```python
str(s)
```




    'SELECT cookies.cookie_id, cookies.cookie_name, cookies.cookie_recipe_url, cookies.cookie_sku, cookies.quantity, cookies.unit_cost \nFROM cookies \nWHERE cookies.cookie_name LIKE :cookie_name_1 AND cookies.quantity = :quantity_1'




```python
s = cookies.select(limit=1)
```


```python
for row in connection.execute(s):
    print(row)
```

    (1, 'chocolate chip', 'http://some.aweso.me/cookie/recipe.html', 'CC01', 12, Decimal('0.50'))
    


```python
s = select([cookies.c.cookie_name, 'SKU-' + cookies.c.cookie_sku])
for row in connection.execute(s):
    print(row)
```

    ('chocolate chip', 'SKU-CC01')
    ('dark chocolate chip', 'SKU-CC02')
    ('peanut butter', 'SKU-PB01')
    ('oatmeal raisin', 'SKU-EWW01')
    


```python
s = select([cookies.c.cookie_name, cookies.c.quantity * cookies.c.unit_cost])
for row in connection.execute(s):
    print('{} - {}'.format(row.cookie_name, row.anon_1))
```

    chocolate chip - 6.00
    dark chocolate chip - 0.75
    peanut butter - 6.00
    oatmeal raisin - 100.00
    


```python
from sqlalchemy import cast
s = select([cookies.c.cookie_name, cast((cookies.c.quantity * cookies.c.unit_cost), Numeric(12, 2)).label('inv_cost')])
for row in connection.execute(s):
    print('{} - {}'.format(row.cookie_name, row.inv_cost))
```

    chocolate chip - 6.00
    dark chocolate chip - 0.75
    peanut butter - 6.00
    oatmeal raisin - 100.00
    


```python
from sqlalchemy import cast
s = select([cookies.c.cookie_name, cast((cookies.c.quantity * cookies.c.unit_cost), Numeric(12, 2)).label('inv_cost')])
for row in connection.execute(s):
    print('{:<25} {:.2f}'.format(row.cookie_name, row.inv_cost))
```

    chocolate chip            6.00
    dark chocolate chip       0.75
    peanut butter             6.00
    oatmeal raisin            100.00
    


```python
from sqlalchemy import and_, or_, not_
s = select([cookies]).where(and_(cookies.c.quantity > 23, cookies.c.unit_cost < 0.40))
for row in connection.execute(s):
    print(row.cookie_name)
```

    peanut butter
    


```python
from sqlalchemy import and_, or_, not_
s = select([cookies]).where(or_(cookies.c.quantity.between(10, 50), cookies.c.cookie_name.contains('chip')))
for row in connection.execute(s):
    print(row.cookie_name)
```

    chocolate chip
    dark chocolate chip
    peanut butter
    


```python
from sqlalchemy import update
u = update(cookies).where(cookies.c.cookie_name == "chocolate chip")
u = u.values(quantity=(cookies.c.quantity + 120))
result = connection.execute(u)
print(result.rowcount)
```

    1
    


```python
s = select([cookies]).where(cookies.c.cookie_name == "chocolate chip")
result = connection.execute(s).first()
for key in result.keys():
    print('{:>20}: {}'.format(key, result[key]))
```

               cookie_id: 1
             cookie_name: chocolate chip
       cookie_recipe_url: http://some.aweso.me/cookie/recipe.html
              cookie_sku: CC01
                quantity: 132
               unit_cost: 0.50
    


```python
from sqlalchemy import delete
u = delete(cookies).where(cookies.c.cookie_name == "dark chocolate chip")
result = connection.execute(u)
print(result.rowcount)
s = select([cookies]).where(cookies.c.cookie_name == "dark chocolate chip")
result = connection.execute(s).fetchall()
print(len(result))
```

    1
    0
    


```python
print(result)
```

    []
    


```python
customer_list = [
    {
        'username': 'cookiemon',
        'email_address': 'mon@cookie.com',
        'phone': '111-111-1111',
        'password': 'password'
    },
    {
        'username': 'cakeeater',
        'email_address': 'cakeeater@cake.com',
        'phone': '222-222-2222',
        'password': 'password' 
    }, 
    {
        'username': 'pieguy',
        'email_address': 'guy@pie.com',
        'phone': '333-333-3333',
        'password': 'password'
    }
]
```


```python
ins = users.insert()
result = connection.execute(ins, customer_list)
```


```python
ins = insert(orders).values(user_id=1, order_id=1)
result = connection.execute(ins)
```


```python
ins = insert(line_items)
order_items = [
    {
        'order_id': 1,
        'cookie_id': 1,
        'quantity': 2,
        'extended_cost': 1.00
    },
    {
        'order_id': 1,
        'cookie_id': 3,
        'quantity': 12,
        'extended_cost': 3.00
    }
]

result = connection.execute(ins, order_items)
```


```python
ins = insert(orders).values(user_id=2, order_id=2)
result = connection.execute(ins)
```


```python
ins = insert(line_items)
order_items = [
    {
        'order_id': 2,
        'cookie_id': 1,
        'quantity': 24,
        'extended_cost': 12.00
    },
    {
        'order_id': 2,
        'cookie_id': 4,
        'quantity': 6,
        'extended_cost': 6.00
    }
]
result = connection.execute(ins, order_items)
```


```python
columns = [orders.c.order_id, users.c.username, users.c.phone, cookies.c.cookie_name, line_items.c.quantity, line_items.c.extended_cost]

cookiemon_orders = select(columns)

cookiemon_orders = cookiemon_orders.select_from(users.join(orders).join(line_items).join(cookies)).where(users.c.username == 'cookiemon')
result = connection.execute(cookiemon_orders).fetchall()

for row in result:
    print(row)
```

    (1, 'cookiemon', '111-111-1111', 'chocolate chip', 2, Decimal('1.00'))
    (1, 'cookiemon', '111-111-1111', 'peanut butter', 12, Decimal('3.00'))
    


```python
str(cookiemon_orders)
```




    'SELECT orders.order_id, users.username, users.phone, cookies.cookie_name, line_items.quantity, line_items.extended_cost \nFROM users JOIN orders ON users.user_id = orders.user_id JOIN line_items ON orders.order_id = line_items.order_id JOIN cookies ON cookies.cookie_id = line_items.cookie_id \nWHERE users.username = :username_1'




```python
columns = [users.c.username, func.count(orders.c.order_id)]
all_orders = select(columns)
all_orders = all_orders.select_from(users.outerjoin(orders)).group_by(users.c.username)
print(str(all_orders))
result = connection.execute(all_orders).fetchall()
for row in result:
    print(row)
```

    SELECT users.username, count(orders.order_id) AS count_1 
    FROM users LEFT OUTER JOIN orders ON users.user_id = orders.user_id GROUP BY users.username
    ('cakeeater', 1)
    ('cookiemon', 1)
    ('pieguy', 0)
    


```python
def get_orders_by_customer(cust_name):
    columns = [orders.c.order_id, users.c.username, users.c.phone, cookies.c.cookie_name, line_items.c.quantity, line_items.c.extended_cost]
    cust_orders = select(columns)
    cust_orders = cust_orders.select_from(users.join(orders).join(line_items).join(cookies)).where(users.c.username == cust_name)
    result = connection.execute(cust_orders).fetchall()
    return result
```


```python
get_orders_by_customer('cakeeater')
```




    [(2, 'cakeeater', '222-222-2222', 'chocolate chip', 24, Decimal('12.00')),
     (2, 'cakeeater', '222-222-2222', 'oatmeal raisin', 6, Decimal('6.00'))]




```python
def get_orders_by_customer(cust_name, shipped=None, details=False):
    columns = [orders.c.order_id, users.c.username, users.c.phone]
    joins = users.join(orders)
    if details:
        columns.extend([cookies.c.cookie_name, line_items.c.quantity, line_items.c.extended_cost])
        joins = joins.join(line_items).join(cookies)
        
    cust_orders = select(columns)
    cust_orders = cust_orders.select_from(joins).where(users.c.username == cust_name)
    if shipped is not None:
        cust_orders = cust_orders.where(orders.c.shipped == shipped)
    result = connection.execute(cust_orders).fetchall()
    return result
```


```python
get_orders_by_customer('cakeeater')
```




    [(2, 'cakeeater', '222-222-2222')]




```python
get_orders_by_customer('cakeeater', details=True)
```




    [(2, 'cakeeater', '222-222-2222', 'chocolate chip', 24, Decimal('12.00')),
     (2, 'cakeeater', '222-222-2222', 'oatmeal raisin', 6, Decimal('6.00'))]




```python
get_orders_by_customer('cakeeater', shipped=True)
```




    []




```python
get_orders_by_customer('cakeeater', shipped=False)
```




    [(2, 'cakeeater', '222-222-2222')]




```python
get_orders_by_customer('cakeeater', shipped=False, details=True)
```




    [(2, 'cakeeater', '222-222-2222', 'chocolate chip', 24, Decimal('12.00')),
     (2, 'cakeeater', '222-222-2222', 'oatmeal raisin', 6, Decimal('6.00'))]




```python
result = connection.execute("select * from orders").fetchall()
print(result)
```

    [(1, 1, 0), (2, 2, 0)]
    


```python
from sqlalchemy import text
stmt = select([users]).where(text('username="cookiemon"'))
print(connection.execute(stmt).fetchall())
```

    [(1, None, 'cookiemon', 'mon@cookie.com', '111-111-1111', 'password', datetime.datetime(2022, 4, 11, 20, 17, 36, 327069), datetime.datetime(2022, 4, 11, 20, 17, 36, 327069))]
    


```python
# Writing SQL statements and interacting with databases in Python reminded me a lot of C#. I enjoyed how in Python, 
# you can mix and match the use of functions and direct statements depending on the use case and personal style. 
# In C#, a similar dynamic exists, where you can use direct SQL statements, or take advantage of LINQ and chain 
# together methods. Unlike Python, mixing and matching these approaches is not as simple. Creating the database 
# locally, directly in the code was similar to SQL room in Kotlin, used for local storage in Android applications. 
# Similar to Python, you created the structures programmatically using structures and defined validation through 
# parameters or methods.
```

## Jonathan Doolittle


```python

```
