#  （译）SQLAlchemy教程

## 译者注

SQLAlchemy是python下的一个对象关系映射（Object Relational Mapper，orm）库。通过对象关系映射我们能轻松的访问数据库而不用自己构造各种sql。。各种sql散布在程序的各个角落就显得很乱。每次都自己写好操作数据库的类又很麻烦。orm就能很好的解决这个问题。不仅如此，用orm写出来的程序能提供数据库无关性。这样程序就可以在装有不同数据库的服务器运行了。

在python的很多orm库中，SQLAlchemy是相对稳定高效的一个，作为一个计科的学生来说，这是一个不错的选择。

原文链接:<https://www.pythoncentral.io/overview-sqlalchemys-expression-language-orm-queries/>

## 概述

在前面的文章中,我们比较了sqlslchemy和各种其他的python的orm.在这篇文章中我们将深入了解sqlAlchemy的orm和语言上的表达并使用一个示例来展示他们的可用的API和易于理解的Python结构。

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

在这个栗子中我们用sqlite数据库在内存中创建了两个表部门和雇员。列‘employee.department_id’是一个外键到列‘department.id’