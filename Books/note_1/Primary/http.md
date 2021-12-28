# linux 命令行玩http
* /dev/tcp/ 路径看不见，但是确实存在
- 与www.baidu.com：80建立socket连接。 <>表示输入输出， 8就是一个数字其他的也行，随意吧。
`exec 8<> /dev/tcp/www.baidu.com/80` 
- $$表示当前解释器进程的ID号
`cd /proc/$$/fd`
```
ls -l
lrwx------ 1 root root 64 May  2 14:52 0 -> /dev/pts/1
lrwx------ 1 root root 64 May  2 14:52 1 -> /dev/pts/1
lrwx------ 1 root root 64 May  2 14:52 2 -> /dev/pts/1
lrwx------ 1 root root 64 May  2 14:52 255 -> /dev/pts/1
lrwx------ 1 root root 64 May  2 14:52 8 -> 'socket:[105191]'
```
- 0 标准输入 1 标准输出 2 标准错误输出 8新建立的
- 关闭  8 -> 'socket:[105191]' ， 重定向符号后跟的不是文件名必须要加一个&
`exec 8>& -`
-  删除8后再建立个9的连接
`exec 9<> /dev/tcp/www.baidu.com/80` 

- 请求
```
// -e 只是为了解析\n，echo 的标准输出现在重定向到9实现了GET请求
echo -e "GET / HTTP/1.0\n" 1>& 9
// 返回到标准输出？
cat 0<& 9
//没数据？间隔时间太久了socket连接关闭了。删除连接再快速来一遍，有数据了吧
```
