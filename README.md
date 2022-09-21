# pymongo_shard
* 1. Pymongo单实例升级分片集群，默认自动开启，不用手动开启库表分片，默认表使用_id作为分片键。
* 2. 解决使用_id分片后，更新和删除需要带上分片列的问题

## 使用示例
```python
from pymongos import ShardMongoClient
from pymongo import UpdateOne,UpdateMany,DeleteMany

mongodbUri = 'mongodb://mongouser:1234567a@localhost:27017/'
client = ShardMongoClient(mongodbUri)
db = client.test

#insert data
db.num.insert_one({'id':1, 'name':'R9', 'des':'pretty'})
db.num.insert_one({'id':2, 'name':'BOY', 'des':'handsome'})
db.num.insert_one({'id':3, 'name':'cat', 'des':'nice'})
db.num.insert_one({'id':4, 'name':'dog', 'des':'clever'})


#update data
db.num.update_one({"name":"R9"},{"$set":{"des":"good"}})

#update many
db.num.bulk_write([UpdateMany({"name":"R9"},{"$set":{"des":"good"}})])


#delete data
db.num.delete_one({"name":"BOY"})

db.num.bulk_write([DeleteMany({"name":"R9"},{"$set":{"des":"good"}})])
```

