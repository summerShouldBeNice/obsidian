1. BIO
	1. 同步并阻塞
	2. 一个连接一个线程 ，客户端请求服务器的时候就会启动一个线程进行连接，如果连接了什么事都不做就会造成不必要的线程开销，而且如果客户端很多那么服务端就要提供相应的线程
	3. **适用于连接数较小且固定的架构**，这种方式对服务器资源的要求比较高，并局限于应用中，jdk1.4以前的唯一选择，程序简单并且易理解
2. NIO
	1. 同步非阻塞
	2. 一个线程可以处理多个请求（连接），客户端发送的请求都会到一个多路复用器上，多路复用器轮询到有i/o连接就处理如果没有就不处理
	3. **适用于连接数较多且固定的架构（轻操作）**，比如聊天服务器，弹幕系统，服务器之间的通讯，编程比较复杂，jdk1.5开始支持
3. AIO
	1. NIO2.0
	2. 异步非阻塞
	3. 一个有效线程一个连接，客户端的i/o请求都是由OS先完成了再通知服务器去启动线程进行处理，一般适用于连接数较多且连接时间较长的应用
	4. **适用于连接数较多且比较长的架构（重操作）**，比如相册服务器，充分调用OS参与并发操作，编程比较复杂，jdk7开始支持