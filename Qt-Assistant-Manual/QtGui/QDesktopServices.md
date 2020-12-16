# QDesktopServices

## 1.Public Types

- `enum	StandardLocation { DesktopLocation, DocumentsLocation, FontsLocation, ApplicationsLocation, ..., CacheLocation }`

  **该枚举描述了`QDesktopServices :: storageLocation`和`QDesktopServices :: displayName`可以查询的不同位置**。

  | Constant                                 | Value | Description                                                  |
  | ---------------------------------------- | ----- | ------------------------------------------------------------ |
  | `QDesktopServices::DesktopLocation`      | 0     | 返回用户的桌面目录。                                         |
  | `QDesktopServices::DocumentsLocation`    | 1     | 返回用户的文档。                                             |
  | `QDesktopServices::FontsLocation`        | 2     | 返回用户的字体                                               |
  | `QDesktopServices::ApplicationsLocation` | 3     | 返回用户的应用                                               |
  | `QDesktopServices::MusicLocation`        | 4     | 返回用户的音乐                                               |
  | `QDesktopServices::MoviesLocation`       | 5     | 返回用户的电影                                               |
  | `QDesktopServices::PicturesLocation`     | 6     | 返回用户的图片                                               |
  | `QDesktopServices::TempLocation`         | 7     | 返回系统的临时目录                                           |
  | `QDesktopServices::HomeLocation`         | 8     | 返回用户的家目录                                             |
  | `QDesktopServices::DataLocation`         | 9     | 返回可以存储持久性应用程序数据的目录位置。 `QCoreApplication :: applicationName`和`QCoreApplication :: organizationName`应该在所有平台上都可以使用。 |
  | `QDesktopServices::CacheLocation`        | 10    | 返回应在其中写入用户特定的非必需（缓存）数据的目录位置。     |

  

## 2.Static Public Members

- `QString	displayName ( StandardLocation type )`

  返回给定位置类型的**本地化显示名称**，如果找不到相关位置，则返回一个空QString。

- `bool	openUrl ( const QUrl & url )`

  在适合用户桌面环境的Web浏览器中打开给定的url，如果成功，则返回true；否则返回false。

  *如果URL是对本地文件的引用（即URL方案是“文件”），则将使用合适的应用程序而不是Web浏览器来打开它*。

  以下示例在Windows文件系统上打开一个文件，该文件位于包含空格的路径上：

  ```c++
  QDesktopServices::openUrl(QUrl("file:///C:/Documents and Settings/All Users/Desktop", QUrl::TolerantMode));
  ```

  如果指定了mailto URL，则将使用用户的电子邮件客户端打开包含URL中指定的选项的编辑器窗口，类似于Web浏览器处理mailto链接的方式。

  例如，以下URL包含收件人（user@foo.com），主题（测试）和消息正文（仅测试）：

  ```c++
  mailto:user@foo.com?subject=Test&body=Just a test
  ```

  警告：尽管许多电子邮件客户端可以发送附件并且支持Unicode，但是用户可能已经配置了没有这些功能的客户端。 另外，某些电子邮件客户端（例如Lotus Notes）在使用长URL时会遇到问题。

  注意：在Symbian OS上，如果Web浏览器已在运行，则需要SwEvent功能才能打开给定的URL。

- `void	setUrlHandler ( const QString & scheme, QObject * receiver, const char * method )`

  将给定方案的处理程序设置为接收器对象提供的处理程序方法。

  此函数提供了一种自定义openUrl（）行为的方法。 如果使用具有指定方案的URL调用openUrl（），则将调用接收方对象上的给定方法，而不是QDesktopServices启动外部应用程序。

  提供的方法必须实现为仅接受单个QUrl参数的插槽。

  如果使用setUrlHandler（）为已经具有处理程序的方案设置新的处理程序，则将现有的处理程序简单地替换为新的处理程序。 由于QDesktopServices不拥有处理程序的所有权，因此在替换处理程序时不会删除任何对象。

  请注意，**将始终从调用QDesktopServices :: openUrl（）的同一线程内调用处理程序**。

- `QString	storageLocation ( StandardLocation type )`

  **返回类型文件所在的默认系统目录**，如果无法确定位置，则返回空字符串。

  注意：返回的存储位置可以是一个不存在的目录。 即可能需要由系统或用户创建。

  注意：在Symbian OS上，ApplicationsLocation始终将/ sys / bin文件夹指向具有可执行文件的同一驱动器。 FontsLocation始终指向ROM驱动器上的文件夹。 Symbian OS没有桌面概念，DesktopLocation返回与DocumentsLocation相同的路径。 其余标准位置指向具有可执行文件的同一驱动器上的文件夹，但如果可执行文件位于ROM中，则返回C驱动器中的文件夹。

- `void	unsetUrlHandler ( const QString & scheme )`

  删除指定方案的先前设置的URL处理程序。

## 3.Detailed Description

QDesktopServices类提供用于访问常见桌面服务的方法。

许多桌面环境提供的服务可被应用程序用来执行常见任务，例如以一致且兼顾用户应用程序首选项的方式打开网页。

此类包含的功能为这些服务提供简单的接口，以指示它们是成功还是失败。

openUrl（）函数用于在外部应用程序中打开位于任意URL的文件。对于与本地归档系统上的资源相对应的URL（URL方案为“文件”），将使用合适的应用程序打开文件；否则，将使用网络浏览器来获取和显示文件。

用户的桌面设置控制是打开某些可执行文件类型进行浏览还是执行它们。一些桌面环境被配置为阻止用户执行从非本地URL获得的文件，或者在执行操作之前征求用户的许可。

### URL Handlers

可以针对单个URL方案自定义openUrl（）函数的行为，以允许应用程序覆盖某些类型的URL的默认处理行为。

分派机制仅允许每个URL方案使用一个自定义处理程序。 这是使用setUrlHandler（）函数设置的。 每个处理程序都实现为仅接受单个QUrl参数的插槽。

可以使用unsetUrlHandler（）函数删除每个方案的现有处理程序。 这会将给定方案的处理行为返回到默认行为。

例如，该系统使实施帮助系统变得容易。 可以使用help：// myapplication / mytopic URL在标签和文本浏览器中提供帮助，并且通过注册处理程序，可以在应用程序内部显示帮助文本：

```c++
 class MyHelpHandler : public QObject
 {
     Q_OBJECT
 public:
     ...
 public slots:
     void showHelp(const QUrl &url);
 };

 QDesktopServices::setUrlHandler("help", helpInstance, "showHelp");
```

如果在处理程序中确定无法打开请求的URL，则可以再次使用相同的参数再次调用QDesktopServices :: openUrl（），它将尝试使用适用于用户桌面环境的机制打开URL。