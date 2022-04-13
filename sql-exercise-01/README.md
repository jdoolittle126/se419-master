```python
from datetime import datetime
from sqlalchemy import (MetaData, Table, Column, Integer, Numeric, String, DateTime, ForeignKey, create_engine)

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
                Column('user_id', ForeignKey('users.user_id')))

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
# In this code, we start off by importing the necessary tools to interact with an SQLite database, 
# as well as some time utilities. We then create 4 tables that represent a basic system in which 
# users can order cookies. Each table has several columns, one of which being the primary key, and 
# the others holding relevant data, such as usernames, order quantity, and costs. as each of these 
# tables are created, they are supplied the ‘metadata’ object. Behind the scenes, the new table object 
# is appended to the metadata object. Finally we create the SQLite engine, and using that engine, call on 
# the metadata object to instantiate all the tables.
```

## Jonathan Doolittle


```python

```
