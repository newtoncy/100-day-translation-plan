#  （译）SQLAlchemy教程

## 译者注

SQLAlchemy是python下的一个对象关系映射（Object Relational Mapper，orm）库。通过对象关系映射我们能轻松的访问数据库而不用自己构造各种sql。。各种sql散布在程序的各个角落就显得很乱。每次都自己写好操作数据库的类又很麻烦。orm就能很好的解决这个问题。不仅如此，用orm写出来的程序能提供数据库无关性。这样程序就可以在装有不同数据库的服务器运行了。

在python的很多orm库中，SQLAlchemy是相对稳定高效的一个，作为一个计科的学生来说，这是一个不错的选择。

原文链接:<https://www.pythoncentral.io/overview-sqlalchemys-expression-language-orm-queries/>

## 概述

在前面的文章中,我们比较了sqlslchemy和各种其他的python的orm.在这篇文章中我们将深入了解sqlAlchemy的orm和语言上的表达并使用一个示例来展示其可用的API和易于理解的Python结构。

sqlalchemy不仅提供了一种映射关系到对象的方法，还提供了一套方便的适合python的查询api。在一个有sqlachemt的数据库中找一个数据是很愉快的事情，因为每一件事情都直接了当，查询结果通过python对象返回，查询参数也是。

sqlalchemy表达语言为程序提供了一套系统来通过python结构体来写“sql定义”。这些构造模型在隐藏不同数据库后端的差异的同时又尽可能的接近数据库底层。虽然这些结构旨在用一致的结构表达等效的后台的概念，但是他们不会掩盖后台有用的具体的功能。因此，这种表达语言提供了一种方法来让程序自然的表达后台的概念。

sql是对象关系映射的补充，而orm展示了一个抽象的描述来将数据库定义映射到python中来，modals用来映射表，关系用来映射通过一个关系表来建立的多对多关系，一对一通过外键。这种表达语言用来直接的表达原始的结构是没有任何争议的。

## 一个部门和雇员的栗子

让我们使用一个栗子来说明如何用表达式语言操作数据库中的两个表：部门和雇员。一个部门有很多部员，部员则往往只属于一个部门。因此，这个数据库可以这样定义：

```python
>>> from sqlalchemy import Column, String, Integer, ForeignKey
>>> from sqlalchemy.orm import relationship, backref
>>> from sqlalchemy.ext.declarative import declarative_base
>>>
>>>
>>> Base = declarative_base()
>>>
>>>
>>> class Department(Base):
>>> ...     __tablename__ = 'department'
>>> ...     id = Column(Integer, primary_key=True)
>>> ...     name = Column(String)
>>> ...
>>>
>>> class Employee(Base):
>>> ...     __tablename__ = 'employee'
>>> ...     id = Column(Integer, primary_key=True)
>>> ...     name = Column(String)
>>> ...     department_id = Column(Integer, ForeignKey('department.id'))
>>> ...     department = relationship(Department, backref=backref('employees', uselist=True))
>>> ...
>>>
>>> from sqlalchemy import create_engine
>>> engine = create_engine('sqlite:///')
>>>
>>> from sqlalchemy.orm import sessionmaker
>>> session = sessionmaker()
>>> session.configure(bind=engine)
>>> Base.metadata.create_all(engine)
```

在这个栗子中我们用sqlite数据库在内存中创建了两个表部门和雇员。列 ‘employee.department_id’ 是一个到列‘department.id’的外键。同时，关系 ‘department.emplyees’ 包含了所有的部门中的部员。为了测试我们的设置，我们可以简单的插入几个记录作为栗子并通过orm检索出来。

```python
>>> john = Employee(name='john')
>>> it_department = Department(name='IT')
>>> john.department = it_department
>>> s = session()
>>> s.add(john)
>>> s.add(it_department)
>>> s.commit()
>>> it = s.query(Department).filter(Department.name == 'IT').one()
>>> it.employees
[]
>>> it.employees[0].name
u'john'
```

就像你看到的那样，我们插入了一个部员，john，加入到了it部门。

> 扩展（译者给自己加戏的部分）：
>
> 参考链接:https://docs.sqlalchemy.org/en/latest/core/metadata.html#sqlalchemy.schema.Column
>
> https://docs.sqlalchemy.org/en/latest/core/constraints.html?highlight=sqlalchemy%20schema%20foreignkey
>
> https://docs.sqlalchemy.org/en/latest/orm/relationship_api.htm
>
> - Column(\*args, \*\*kwargs)
>
>   name -列的名字
>
>   type -  类型
>
>   \*args-  看不懂
>
>   autoincrement- 自增,主键为整形时默认值为"auto",可以设定为True表示自增或设置为False
>
>   default - 默认值
>
>   index - true或false,是否建索引
>
>   nullable - 可为空
>
>   primary_key - 是否为主键
>
>   unique - 不重复
>
> - ForeignKey("表名.列名",...)外键约束
>
>   onupdate 和 ondelete - "cascade"级联删除 "restrict"和"no action"不准删 "set null"设为空
>
> - relationship

现在，我们用表达式语言来演示一些查询。
```python
>>> from sqlalchemy import select
>>> find_it = select([Department.id]).where(Department.name == 'IT')
>>> rs = s.execute(find_it)
>>> rs
 
>>> rs.fetchone()
(1,)
>>> rs.fetchone()  # Only one result is returned from the query, so getting one more returns None.
>>> rs.fetchone()  # Since the previous fetchone() returned None, fetching more would lead to a result-closed exception
Traceback (most recent call last):
  File "", line 1, in 
  File "/Users/xiaonuogantan/python2-workspace/lib/python2.7/site-packages/sqlalchemy/engine/result.py", line 790, in fetchone
    self.cursor, self.context)
  File "/Users/xiaonuogantan/python2-workspace/lib/python2.7/site-packages/sqlalchemy/engine/base.py", line 1027, in _handle_dbapi_exception
    util.reraise(*exc_info)
  File "/Users/xiaonuogantan/python2-workspace/lib/python2.7/site-packages/sqlalchemy/engine/result.py", line 781, in fetchone
    row = self._fetchone_impl()
  File "/Users/xiaonuogantan/python2-workspace/lib/python2.7/site-packages/sqlalchemy/engine/result.py", line 700, in _fetchone_impl
    self._non_result()
  File "/Users/xiaonuogantan/python2-workspace/lib/python2.7/site-packages/sqlalchemy/engine/result.py", line 724, in _non_result
    raise exc.ResourceClosedError("This result object is closed.")
sqlalchemy.exc.ResourceClosedError: This result object is closed.
>>> find_john = select([Employee.id]).where(Employee.department_id == 1)
>>> rs = s.execute(find_john)
 
>>> rs.fetchone()  # Employee John's ID
(1,)
>>> rs.fetchone()
```

因为表达式语言提供了类似于后台的sql的低级的python结构,所以他们用起来感觉就和在写真正的sql一样,只是更加python

## 部员和部门的多对多关系

在之前的栗子,似乎一个部员只能属于最多一个部门.如果一个部员能属于多个部门呢?这是不是说一个外键就表达不了这种关系了呢?

是的,一个外键是不够的.为了定义一个在部员和部门之间的多对多关系我们创建一个新的具有两个外键的关联表,一个叫'department.id'一个叫'employee.id'

```python
>>> from sqlalchemy import Column, String, Integer, ForeignKey
>>> from sqlalchemy.orm import relationship, backref
>>> from sqlalchemy.ext.declarative import declarative_base
>>>
>>>
>>> Base = declarative_base()
>>>
>>>
>>> class Department(Base):
...     __tablename__ = 'department'
...     id = Column(Integer, primary_key=True)
...     name = Column(String)
...     employees = relationship('Employee', secondary='department_employee')
...
>>>
>>> class Employee(Base):
...     __tablename__ = 'employee'
...     id = Column(Integer, primary_key=True)
...     name = Column(String)
...     departments = relationship('Department', secondary='department_employee')
...
>>>
>>> class DepartmentEmployee(Base):
...     __tablename__ = 'department_employee'
...     department_id = Column(Integer, ForeignKey('department.id'), primary_key=True)
...     employee_id = Column(Integer, ForeignKey('employee.id'), primary_key=True)
...
>>> from sqlalchemy import create_engine
>>> engine = create_engine('sqlite:///')
>>> from sqlalchemy.orm import sessionmaker
>>> session = sessionmaker()
>>> session.configure(bind=engine)
>>> Base.metadata.create_all(engine)
>>>
>>> s = session()
>>> john = Employee(name='john')
>>> s.add(john)
>>> it_department = Department(name='IT')
>>> it_department.employees.append(john)
>>> s.add(it_department)
>>> s.commit()
```

在上面这个栗子中,我们创建了一个关系表,有两个外键.这个关系表'department_employee' 连结了'department' 和 'employee' ....后面一堆罗里吧嗦的话

我们可以用下面的查询测试我们的设置

```python
>>> john = s.query(Employee).filter(Employee.name == 'john').one()
>>> john.departments
[]
>>> john.departments[0].name
u'IT'
>>> it = s.query(Department).filter(Department.name == 'IT').one()
>>> it.employees
[]
>>> it.employees[0].name
u'john'
```

现在我们插入一个部员和另一个部门在db中

```python
>>> marry = Employee(name='marry')
>>> financial_department = Department(name='financial')
>>> financial_department.employees.append(marry)
>>> s.add(marry)
>>> s.add(financial_department)
>>> s.commit()

```

找到所有属于IT部门的,我们可以这样:

```python
>>> s.query(Employee).filter(Employee.departments.any(Department.name == 'IT')).one().name
u'john'
```

或者使用表达式语言

```python
>>> find_employees = select([DepartmentEmployee.employee_id]).select_from(Department.__table__.join(DepartmentEmployee)).where(Department.name == 'IT')
>>> rs = s.execute(find_employees)
>>> rs.fetchone()
(1,)
>>> rs.fetchone()
```

