# QUdpSocket

继承关系：`QUdpSocket`->`QAbstractSocket`->`QIODevice`->`QObject`

## 1.Public Functions

- QUdpSocket(QObject *parent = nullptr)
- virtual ~QUdpSocket()
- bool hasPendingDatagrams() const
- bool joinMulticastGroup(const QHostAddress &groupAddress)
- bool joinMulticastGroup(const QHostAddress &groupAddress, const QNetworkInterface &iface)
- bool leaveMulticastGroup(const QHostAddress &groupAddress)
- bool leaveMulticastGroup(const QHostAddress &groupAddress, const QNetworkInterface &iface)
- QNetworkInterface multicastInterface() const
- qint64 pendingDatagramSize() const
- qint64 readDatagram(char *data, qint64 maxSize, QHostAddress *address = nullptr, quint16 *port = nullptr)
- QNetworkDatagram receiveDatagram(qint64 maxSize = -1)
- void setMulticastInterface(const QNetworkInterface &iface)
- qint64 writeDatagram(const char *data, qint64 size, const QHostAddress &address, quint16 port)
- qint64 writeDatagram(const QNetworkDatagram &datagram)
- qint64 writeDatagram(const QByteArray &datagram, const QHostAddress &host, quint16 port)

## 2.Detailed Description