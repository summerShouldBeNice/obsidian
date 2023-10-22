## 基本指令 
1. show dbs / show databases 
	1. 显示所有数据库
2. use  数据库名
	1. 进入到指定数据库内 
3. db
	1. 显示当前所在的数据库
4. show collections
	1. 显示当前数据库下的所有集合
5. db.collection.drop()
	1. 删除当前集合下的所有文档
6. db.dropDatabase()
	1. 删除数据库
## 数据库的crud操作
- 插入
	- db.collection.insert(doc)
		- 在当前集合下插入单个文档
	- db.collection.insertOne(doc)
		- 在当前集合下插入单个文档
	- db.collection.insertMany(doc)
		- 在当前集合下插入多个文档
- 查找
	- db.collection.find()
		- 查找当前符合条件的所有文档
	- db.collection.findOne()
		- 查询当前符合条件的第一个文档
	- db.collection.find().count()
		- 查询当前符合条件的所有文档数量
- 修改
	- db.collection.update(查询条件，新对象)
		- 修改根据查询条件查询到的符合查询条件的对象
		- *example:* db.users.update({"username" : "warmwind"}, {[[operator]]:{"password" : "2693387413"}})
	- db.collection.updateOne(查询条件，新对象)
		- 修改根据查询条件查询到的符合查询条件的对象
	- db.collection.updateMany(查询条件，新对象)
		- 同时修改根据查询条件查询到的符合查询条件的对象
- 删除
	- db.collection.remove(条件)
		- 根据条件删除，默认条件下删除多个，如果为空则清空集合
	- db.colletion.deleteOne()
		- 根据条件删除一个
	- db.colletion.deleteMany()
		- 根据条件删除多个