
--- 
title:  SQLAlchemy的同步和异步的代码对比 
tags: []
categories: [] 

---
#### 1、engine的区别

在普通的SQLAlchemy中，建立engine对象，我们会采用下面的方式:

```
from sqlalchemy import create_engine
engine = create_engine(SQLALCHEMY_DATABASE_URI, pool_recycle=1500)

```

而异步的方式如下:

```
from sqlalchemy.ext.asyncio import create_async_engine
async_engine = create_async_engine(ASYNC_SQLALCHEMY_URI, pool_recycle=1500)

```

#### 2、session的区别

我们一般用sessionmaker来建立session，不过异步的有点区别:

```
from sqlalchemy.ext.asyncio import AsyncSession
from sqlalchemy.orm import sessionmaker

# 同步session
Session = sessionmaker(engine)

# 异步session 区别在于需要指定对应的class_
async_session = sessionmaker(async_engine, class_=AsyncSession)

```

#### 3、建立会话

我们还是以代码的形式展示:

```
# 同步
with Session() as session:
  # 里面是具体的sql操作
  pass
  
# 异步
async with Session() as session:
    # 里面是异步的操作，区别就是从with变成了async with 也就意味着方法必须是async修饰的
    pass

```

#### 4、查询

新老版本的对比:

```
# 注意Session为同步Session，为了区分，异步session为async_session
# model则为具体的Model类

# 异步查询方式
from sqlalchemy import select


async def query():
    async with async_session() as session:
        sql = select(model).where(model.id == 1)
        print(sql) # 这里可以打印出sql
        result = await session.execute(sql)
        # 第一条数据
        data = result.scalars().first()
        # 所有数据
        # data = result.scalars().all()


# 同步查询方式一
def query():
    with Session() as session:
        # 查询id=1的第一条数据 result对应的就是model的实例 如果没有则是None
        result = session.query(model).filter_by(id=1).first()
        # 查询所有数据 result对应的数据为List[model]，即model数组
        # result = session.query(model).filter_by(name="zhangsan").all()

# 同步查询方式二
def query():
    with Session() as session:
        # 查询id=1的第一条数据 result对应的就是model的实例 如果没有则是None
        result = session.query(model).filter(model.id == 1).first()
        # 查询所有数据 result对应的数据为List[model]，即model数组
        # result = session.query(model).filter(model.name == "zhangsan").all()

```

#### 5、新增

这里开始就只讲异步的操作了。

```
async def insert(data):
    async with async_session() as session:
        async with session.begin():
            session.add(data)
            # 刷新自带的主键
            await session.flush()
            # 释放这个data数据
            session.expunge(data)
            return data

```

先说一下session.begin，这个你可以理解为一个事务操作，当采用session的begin方法后，你可以发现我们不需要调用commit方法也能把修改存入数据库。

expunge方法，是用例释放这个实例，SQLAlchemy有个特点，当你的session会话结束以后，它会销毁你插入的这种临时数据，你再想访问这个data就访问不了了。所以我们可以释放这个数据。（expunge的作用）

#### 6、编辑

一般编辑有2种方式:
- 查询出对应的数据，在数据上修改- 根据key-value的形式，修改对应数据的字段
```
from sqlalchemy import select, update

# 方式一
async def update_record(model):
    async with async_session() as session:
        async with session.begin():
            result = await session.execute(select(model).where(id=1))
            now = result.scalars().first()
            if now is None:
                raise Exception("记录不存在")
            now.name = "李四"
            now.age = 23
            # 这里测试过，如果去掉flush会导致数据不更新
            await session.flush()
            session.expunge(now)
            return now

# 方式二
async def update_by_map():
    async with async_session() as session:
        async with session.begin():
            # 更新id为1的数据，并把name改为李四 age改为23
            sql = update(model).where(model.id == 1).values(name="李四", age=23)
            await session.execute(sql)

```

#### 7、删除

删除的话，软删除大家都是update，所以不需要多说，物理删除的话，也有两种方式:、
- 查到以后删除之- 直接根据条件删除（这种我没有仔细研究，我选的是第一种方式，容错率高点）
```
async def delete_by_id():
    async with async_session() as session:
        async with session.begin():
            result = await session.execute(select(model).where(model.id == 2))
            original = result.scalars().first()
            if original is None:
                raise Exception("记录不存在")
            # 如果是多条
            # session.delete(original)
            # for item in result:
            #     session.delete(item)

```

希望对大家有帮助~~~

sqlalchemy官网：
