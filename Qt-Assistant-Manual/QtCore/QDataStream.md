# QDataStream

`void QDataStream::setVersion(int v)`

将数据序列化格式的版本号设置为v，即Version枚举的值。
如果您使用的是当前版本的Qt，则不必设置版本，但是**对于您自己的自定义二进制格式，我们建议您这样做**。
为了适应新功能，某些Qt类的数据流序列化格式在某些版本的Qt中已更改。 如果要读取由早期版本的Qt创建的数据，或写入可以由使用早期版本的Qt编译的程序读取的数据，请使用此函数修改QDataStream使用的序列化格式。