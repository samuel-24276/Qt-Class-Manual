# QTcpServer

# 1.Detailed Description

此类可以接收传入的TCP连接。您可以指定端口或让QTcpServer自动选择一个。您可以监听特定地址或所有机器的地址。
调用listen（）以使服务器监听传入的连接。每次客户端连接到服务器时，都会发出newConnection（）信号。
调用nextPendingConnection（）以接受挂起(pending)的连接作为已连接的QTcpSocket。该函数返回指向QAbstractSocket :: ConnectedState中的QTcpSocket的指针，可用于与客户端进行通信。
如果发生错误，则serverError（）返回错误的类型，并且可以调用errorString（）以获得对所发生事件的易于理解的描述。
监听连接时，服务器正在监听的地址和端口可作为serverAddress（）和serverPort（）使用。
调用close（）使QTcpServer停止监听传入的连接。
尽管QTcpServer主要设计用于事件循环，但也可以不使用事件循环。在这种情况下，您必须使用waitForNewConnection（），该阻塞将一直阻塞直到可用连接或超时到期为止。

# 2.Public Functions

## 2.1.`QTcpServer(QObject *parent = nullptr)`

## 2.2.`virtual ~QTcpServer()`

## 2.3.`void close()`

关闭服务器，服务器将不再监听传入的连接

## 2.4.`QString errorString() const`

返回可读的最后发生的错误的描述。

## 2.5.`virtual bool hasPendingConnections() const`

如果服务器具有挂起的连接，则返回true；否则，返回false。

## 2.6.`bool isListening() const`

如果服务器当前在监听传入的连接，则返回true；否则，返回false。

## 2.7.`bool listen(const QHostAddress &address = QHostAddress::Any, quint16 port = 0)`

告诉服务器监听在地址address和端口port上传入的连接。 如果port为0，则自动选择一个端口。 如果address为QHostAddress :: Any，则服务器将在所有网络接口上监听。
成功返回true； 否则返回false

## 2.8.`int maxPendingConnections() const`

返回待处理的已接收连接的最大数目。 默认值为30。

## 2.9.`virtual QTcpSocket* nextPendingConnection()`

返回下一个挂起(pending)的连接，作为连接的QTcpSocket套接字对象。
**套接字是作为服务器的child创建的，这意味着销毁QTcpServer对象时会自动删除该套接字。 最好在完成处理后显式删除该对象，以避免浪费内存**。
如果没有挂起的连接时调用此函数，则返回nullptr。
注意：**返回的QTcpSocket对象不能从另一个线程使用。 如果要使用来自另一个线程的传入连接，则需要重写incomingConnection()**。

## 2.10.`void pauseAccepting()`

暂停接受新的连接。 已在队列的的连接将保留在队列中

## 2.11.`QNetworkProxy proxy() const`

返回此套接字的网络代理。 默认情况下，使用`QNetworkProxy :: DefaultProxy`。

## 2.12.`void resumeAccepting()`

恢复接受新连接。

## 2.13.`QHostAddress serverAddress() const`

如果服务器正在监听连接，则返回服务器的地址。 否则返回`QHostAddress :: Null`。

## 2.14.`QAbstractSocket::SocketError serverError() const`

返回最后发生错误的错误代码。

## 2.15.`quint16 serverPort() const`

如果服务器在监听连接，返回服务器监听的端口号，否则返回0

## 2.16.`void setMaxPendingConnections(int numConnections)`

将待处理的接受连接的最大数量设置为numConnections。 在调用`nextPendingConnection（）`之前，QTcpServer最多接受numConnections个传入连接。 默认情况下，该限制为30个挂起的连接。
服务器达到其最大挂起连接数后，客户端仍可能能够连接（即QTcpSocket仍可以发出connectd（）信号）。 QTcpServer将停止接受新连接，但是操作系统可能仍将它们保持在队列中

## 2.17.`void setProxy(const QNetworkProxy &networkProxy)`

将此套接字的显式网络代理设置为networkProxy。
要禁用对此套接字使用代理，请使用`QNetworkProxy :: NoProxy`代理类型：

`server->setProxy(QNetworkProxy::NoProxy);`

## 2.18.`bool setSocketDescriptor(qintptr socketDescriptor)`

设置服务器描述符，以监听与socketDescriptor的传入连接时应使用的套接字描述符。 如果成功设置了套接字，则返回true；否则，返回false。 
假定套接字处于侦听状态。

## 2.19.`qintptr socketDescriptor() const`

返回服务器用于监听传入指令的本机套接字描述符；如果服务器未监听，则返回-1。
如果服务器使用的是QNetworkProxy，则返回的描述符可能无法与本机套接字函数（native socket functions）一起使用。

## 2.20.`bool waitForNewConnection(int msec = 0, bool *timedOut = nullptr)`

等待最多毫秒（毫秒）或直到传入连接可用。 如果连接可用，则返回true；否则返回false。 如果操作超时并且timedOut不是nullptr，则* timedOut将设置为true。
**这是一个阻塞函数调用。 在单线程GUI应用程序中不建议使用它，因为整个应用程序将停止响应，直到函数返回为止。 当没有事件循环可用时，waitForNewConnection（）最有用**。
非阻塞替代方法是连接到newConnection（）信号。
如果毫秒为-1，则此功能不会超时。

# 3.Signals

## 3.1.`void acceptError(QAbstractSocket::SocketError socketError)`

接受新连接导致错误时，将发出此信号。 socketError参数描述了发生的错误的类型。

## 3.2.`void newConnection()`

每当有新的连接可用时，都会发出此信号。

# 4.Protected Functions

## 4.1.`void addPendingConnection(QTcpSocket *socket)`

QTcpServer :: incomingConnection（）调用此函数以将套接字添加到待处理传入连接的列表中。
注意：如果您不想破坏Pending Connections机制，请不要忘记从重新实现的来回调用该成员。

## 4.2.`virtual void incomingConnection(qintptr socketDescriptor)`

当新连接可用时，此虚拟函数由QTcpServer调用。 socketDescriptor参数是接受的连接的本机套接字描述符。
基本实现创建一个QTcpSocket，设置套接字描述符，然后将QTcpSocket存储在待处理(pending)连接的内部列表中。最后，将发出newConnection（）。
**重新实现此功能，以在连接可用时更改服务器的行为。**
如果此服务器使用的是QNetworkProxy，则socketDescriptor可能无法与本机套接字函数一起使用，而应仅与QTcpSocket :: setSocketDescriptor（）一起使用。
注意：如果在重新实现此方法时创建了另一个套接字，则需要通过调用addPendingConnection（）将其添加到“挂起连接”机制中。
注意：如果要在另一个线程中将传入连接作为新的QTcpSocket对象处理，则必须将socketDescriptor传递给另一个线程，然后在该线程中创建QTcpSocket对象并使用其setSocketDescriptor（）方法。

