# QTcpSocket

> 继承自QAbstractSocket类，QAbstractSocket继承自QIODevice类

# 1.Public Types



| enum  | [BindFlag](qabstractsocket.html#BindFlag-enum) { ShareAddress, DontShareAddress, ReuseAddressHint, DefaultForPlatform } |
| ----- | ------------------------------------------------------------ |
| flags | [BindMode](qabstractsocket.html#BindFlag-enum)               |
| enum  | [NetworkLayerProtocol](qabstractsocket.html#NetworkLayerProtocol-enum) { IPv4Protocol, IPv6Protocol, AnyIPProtocol, UnknownNetworkLayerProtocol } |
| enum  | [PauseMode](qabstractsocket.html#PauseMode-enum) { PauseNever, PauseOnSslErrors } |
| flags | [PauseModes](qabstractsocket.html#PauseMode-enum)            |
| enum  | [SocketError](qabstractsocket.html#SocketError-enum) { ConnectionRefusedError, RemoteHostClosedError, HostNotFoundError, SocketAccessError, SocketResourceError, …, UnknownSocketError } |
| enum  | [SocketOption](qabstractsocket.html#SocketOption-enum) { LowDelayOption, KeepAliveOption, MulticastTtlOption, MulticastLoopbackOption, TypeOfServiceOption, …, PathMtuSocketOption } |
| enum  | [SocketState](qabstractsocket.html#SocketState-enum) { UnconnectedState, HostLookupState, ConnectingState, ConnectedState, BoundState, …, ListeningState } |
| enum  | [SocketType](qabstractsocket.html#SocketType-enum) { TcpSocket, UdpSocket, SctpSocket, UnknownSocketType } |

# 2.Public Functions

## 2.1.构造函数

`QAbstractSocket::QAbstractSocket(QAbstractSocket::SocketType socketType, QObject *parent)`

创建类型为socketType的新抽象套接字。 父参数传递给QObject的构造函数。

## 2.2.中止函数abort()

`void QAbstractSocket::abort()`

中止当前连接并重置套接字。 与disconnectFromHost（）不同，此函数**立即关闭套接字，并丢弃写缓冲区中的所有待处理数据**。

## 2.3.绑定函数bind()

`bool QAbstractSocket::bind(const QHostAddress &address, quint16 port = 0, QAbstractSocket::BindMode mode = DefaultForPlatform)`

使用BindMode模式绑定到端口port上的地址。
**对于UDP套接字**，绑定后，只要UDP数据报到达指定的地址和端口，就会发出信号QUdpSocket :: readyRead（）。 因此，此功能**对于编写UDP服务器很有用**。
**对于TCP套接字**，此功能可用于指定将哪个接口用于传出连接，这**在多个网络接口的情况下很有用**。
默认情况下，使用DefaultForPlatform BindMode绑定套接字。 如果未指定端口，则选择一个随机端口。
成功后，函数返回true，套接字进入BoundState； 否则返回false。

`bool QAbstractSocket::bind(quint16 port = 0, QAbstractSocket::BindMode mode = DefaultForPlatform)`

使用BindMode模式绑定到QHostAddress：无论在哪个端口port上。
默认情况下，使用DefaultForPlatform BindMode绑定套接字。 如果未指定端口，则选择一个随机端口。

## 2.4.连接主机虚函数connectToHost()

`virtual void 
connectToHost(const QString &hostName, quint16 port, QIODevice::OpenMode openMode = ReadWrite, QAbstractSocket::NetworkLayerProtocol protocol = AnyIPProtocol)`

`virtual void 
connectToHost(const QHostAddress &address, quint16 port, QIODevice::OpenMode openMode = ReadWrite)`

尝试连接到端口port上的地址，是一个重载函数。

## 2.5.断开主机连接的函数disconnectFromHost()

`[virtual] void QAbstractSocket::disconnectFromHost()`

尝试关闭socket。 如果有等待写入的等待数据，QAbstractSocket将进入ClosingState并等待直到所有数据都被写入。 最终，它将进入UnconnectedState并发出offlineed（）信号。

## 信号readyRead()

`[signal] void QIODevice::readyRead()`

每当有可用的新数据能够从设备的当前读取通道读取时，都会发出此信号。 仅当有新数据可用时（例如，当网络套接字上有新的网络数据有效负载时，或将新的数据块附加到设备上时），才会再次发出该信号。

readyRead（）不会递归地发出； 如果您重新进入事件循环或在连接到readyRead（）信号的插槽内调用waitForReadyRead（），则不会重新发出该信号（尽管waitForReadyRead（）可能仍返回true）。
对于实现从QIODevice派生的类的开发人员请注意：当新数据到达时，您应始终发出readyRead（）（不要仅因为缓冲区中仍有待读取的数据而发出它）。 在其他情况下不要发出readyRead（）。

## 重写的的函数atEnd()

`virtual bool atEnd() const override`