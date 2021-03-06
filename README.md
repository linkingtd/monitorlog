## 用途

主要用于对项目产生的日志进行跟踪，并将日志发送给回调函数进行处理。本项目中
是 errmailcb.py 处理，找到其中特定正则表达式的行搜集到一起并发送给运维同学。
你可以按照你自己的处理逻辑来处理，只需要引入 tail.py 即可。

## 特点

tail.py 中有一个 `Tail` 类处理跟踪日志文件，每次尝试读取一行的数据，如果不足
一行将不把数据传递给回调函数。Tail 保证传递给回调函数的都是完整的行。Tail 内部
有指针记录当前读取到了哪个位置，因此，在运行过程中不会重复读取，并且日志产生
很慢的情况下会自行休眠，等待下一次读取。目前默认的休眠时间是 60s 。

tail.py 还有一个 tails 函数，会对以当前时间进行格式化文件名的文件进行处理。
如果文件不存在则会休眠 120s 再继续尝试。而且因为是对当前时间进行格式化，当
日志更换日期时能够持续跟踪。

本项目一次只能单线程跟踪一个日志文件。需要多个文件则需要启动多个进程。
