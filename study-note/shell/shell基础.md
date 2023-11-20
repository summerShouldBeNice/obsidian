***
## shell基本概念
	1. shell的作用是解释用户输入的命令或程序
	2. 用户输入一条命令，shell就解释一条
	3. 键盘输入命令，linux给予响应的结果，称之为交互式
	4. shell是一块包裹着系统核心的壳，处于操作系统最外层；
	5. 机器硬件 => 操作系统核心 => shell解释器 => 外围应用程序
## shell脚本编程
1. shell脚本一般使用vim编辑器进行编辑
2. 一般shell脚本的第一行会写 #! /bin/bash；#！是shebang用于指定当前脚本的解释器
```shell
#!/bin/zsh

#this is my fitst shell

echo "hello world"
```
3. echo $SHELL  输出当前shell的解释器
4. linux一切皆文件 ，shell可以很方便的进行文本处理
5. shell脚本定义的变量默认的都是字符串类型
6. cat /etc/shells 输出当前机器支持的shell
***
## shell 命令
1. history命令
	1. history -c 清除历史
	2. history -r 恢复历史
	3. 调用历史记录命令： history显示命令  !历史id 快速执行历史id
	4. !! 执行上次的命令
	5. echo $HISTSIZE 输出历史命令条数
	6. echo $HISTFILE 输出历史命令的存储文件
2. 语言特性
	1. 文件路径tab补全
	2. 命令补全
	3. 快捷键ctrl+a,e,u,r
	4. 通配符
	5. 命令历史
	6. 命令别名
	7. 命令行展开 
3. 变量
	1. name="qjf" echo $name
	2. 变量和值之间不能有空格 
	3. '不能识别特殊变量
	4. “能识别特殊变量
	5. $? 特殊变量 输出上一个命令执行是否正确
	6. 开启子shell的执行方式 bash ./create_var.sh | sh .create_var.sh
		1. 比如定义了一个变量name=18，然后定义了一个shell脚本命令为name=19，如果开启子shell的执行方式去执行，输出echo $name输出的还是18
	7. 不开启子shell的执行方式source ./create_var.sh
		1. 如果使用不开启子shell的执行方式去执行，输出的是19
	8. 反引号 命令 反引号 会将命令执行的结果返回给变量name=反引号whoami反引号
4. 环境变量
	1.   用export内置命令导出的变量，shell通过环境变量确定登录的用户名，PATH路径，文件系统等各种应用