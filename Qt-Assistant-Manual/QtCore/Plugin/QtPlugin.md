# QtPlugin

<QtPlugin>头文件定义用于定义插件的宏。

## Macros宏

- **`Q_DECLARE_INTERFACE ( ClassName, Identifier )`**

  此宏将给定的标识符（ClassName）与名为ClassName的接口类相关联(**关联接口ClassName和接口的子类**)。 标识符必须是唯一的。 例如：

  ```c++
  Q_DECLARE_INTERFACE(BrushInterface,
                      "com.trolltech.PlugAndPaint.BrushInterface/1.0")
  ```

  通常在头文件的ClassName类定义之后立即使用此宏(如继承接口的子类在Q_OBJECT宏之后使用该宏)。 有关详细信息，请参见即插即用示例。

  如果要对命名空间中声明的接口类使用Q_DECLARE_INTERFACE，则必须确保Q_DECLARE_INTERFACE不在命名空间中。 例如：

  ```c++
  namespace Foo
  {
      struct MyInterface { ... };
  }
  
  Q_DECLARE_INTERFACE(Foo::MyInterface, "org.examples.MyInterface")
  ```

- **`Q_EXPORT_PLUGIN2 ( PluginName, ClassName )`**

  此宏为PluginName指定的插件**导出插件类**ClassName。 PluginName的值应对应于插件项目文件中指定的TARGET。

  在Qt插件的源代码中，**该宏应该恰好出现一次，应该在编写实现的地方而不是在头文件中使用**。

  例：

  ```c++
  Q_EXPORT_PLUGIN2(pnp_extrafilters, ExtraFiltersPlugin)
  ```

- `Q_IMPORT_PLUGIN ( PluginName )`

  此宏将导入名为PluginName的插件，该插件与插件的项目文件中指定的TARGET相对应。

  **将此宏插入到应用程序的源代码中将使您能够使用静态插件**。

  例：

  ```c++
   Q_IMPORT_PLUGIN(qjpeg)
  ```

  构建应用程序时，链接器还必须包含静态插件。 对于Qt的预定义插件，您可以使用QTPLUGIN将所需的插件添加到构建中。 例如：

  ```c++
   TEMPLATE      = app
   QTPLUGIN     += qjpeg qgif qmng    # image formats
  ```

  