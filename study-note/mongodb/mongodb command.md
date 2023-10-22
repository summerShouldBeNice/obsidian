## 基本指令 
1. show dbs / show databases 
	1. 显示所有数据库
2. use  数据库名
	1. 进入到指定数据库内 
3. db
	1. 显示当前所在的数据库
4. show collections
	1. 显示当前数据库下的所有集合
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
		- 查找当前集合下的所有文档