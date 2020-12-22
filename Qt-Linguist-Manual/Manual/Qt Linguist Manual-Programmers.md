# Qt Linguist Manual:Programmers

> 在项目的.pro文件里添加以下代码：
>
> `TRANSLATIONS = aboutus_ch.ts`
>
> 最好将该行代码放在RESOURCE下方，方便寻找，翻译文件ts的命名为项目名+下划线+翻译后的语言，有了这行代码后，执行工具->外部->Qt语言家->lupdate更新翻译，即可生成对应的翻译文件，再用Qt Linguist打开ts文件，进行翻译，翻译完成后保存->发布，返回Qt的工具->外部->Qt语言家->lrelease发布翻译步骤，生成对应的qm二进制翻译文件，翻译完成。

在Qt应用程序中，对多种语言的支持非常简单，并且对程序员的工作量几乎没有增加开销。

Qt通过在创建每个窗口时翻译短语来最大程度地减少使用翻译的性能成本。 在大多数应用程序中，**主窗口仅创建一次。 对话框通常创建一次，然后根据需要显示和隐藏**。 *初始翻译一旦完成，翻译后的窗口将不再有运行时开销。 只有那些创建，销毁和随后创建的窗口才需要翻译*。

使用Qt可以创建可以在运行时切换语言的应用程序，但是需要一定数量的程序员干预，这当然会导致运行时性能损失。

## 1.Making the Application Translation-Aware

程序员应让其应用程序查找并加载适当的翻译文件，并将用户可见的文本和Ctrl键盘加速器标记为翻译目标。

每条需要翻译的文本都需要上下文，以帮助翻译人员识别文本在程序中的位置。 在需要相同翻译的多个相同文本的情况下，翻译人员还需要一些信息来消除源文本的歧义。 将文本标记为翻译将自动使类名称用作基本上下文信息。 在某些情况下，程序员可能需要添加其他信息来帮助翻译人员。

### Creating Translation Files

翻译文件包含应用程序中所有用户可见的文本和Ctrl键加速器以及该文本的翻译。 翻译文件的创建如下：

- 首先运行lupdate，以生成第一组TS翻译源文件，其中包含所有用户可见的文本，但不包含翻译。
- TS文件将提供给使用Qt语言学家添加翻译的翻译人员。 Qt Linguist负责任何更改或删除的源文本。
- 运行lupdate以合并添加到应用程序中的所有新文本。 lupdate将应用程序中用户可见的文本与翻译同步； 它不会破坏任何数据。
- 根据需要重复执行步骤2和3。
- 当需要发布应用程序时，将运行lrelease以读取TS文件并在运行时生成应用程序使用的QM文件。

为了使lupdate成功工作，它必须知道要生成哪些翻译文件。 这些文件仅列在应用程序的.pro Qt项目文件中，例如：

```c++
 TRANSLATIONS = arrowpad_fr.ts \
                arrowpad_nl.ts
```

如果您的源包含真正的非Latin1字符串，则需要使用以下行在.pro文件中告知lupdate，例如，以下行：

```
 CODECFORTR = UTF-8
```

### Loading Translations

```c++
 int main(int argc, char *argv[])
 {
     QApplication app(argc, argv);

     QTranslator translator;
     translator.load("hellotr_la");
     app.installTranslator(&translator);
```

对于可识别翻译的应用程序，将创建一个翻译器对象，加载翻译并将翻译器对象安装到应用程序中。

```c++
 int main(int argc, char *argv[])
 {
     QApplication app(argc, argv);

     QString locale = QLocale::system().name();

     QTranslator translator;
     translator.load(QString("arrowpad_") + locale);
     app.installTranslator(&translator);
```

对于源中的非Latin1字符串，您还需要例如：

```c++
QTextCodec::setCodecForTr(QTextCodec::codecForName("utf8"));
```

在生产应用程序中，更灵活的方法（例如，根据语言环境加载翻译）可能更合适。 如果所有TS文件均按照诸如appname_locale之类的约定命名，例如 tt2_fr，tt2_de等，那么上面的代码将在运行时加载当前语言环境的翻译。

如果当前语言环境没有翻译文件，则应用程序将退回到使用原始源文本的位置。

请注意，如果需要在运行时以编程方式添加翻译，则可以重新实现QTranslator :: translate（）。

### Making the Application Translate User-Visible Strings

通过将用户可见的字符串包装在tr（）调用中，可以将它们标记为翻译目标，例如：

```c++
 button = new QPushButton(tr("&Quit"), this);
```

使用Q_OBJECT宏的所有QObject子类都实现tr（）函数。

尽管由于通常被称为QObject子类的成员函数而通常直接进行tr（）调用，但是在其他情况下，可以提供显式的类名，例如：

```c++
 QPushButton::tr("&Quit")
```

### Distinguishing Between Identical Translatable Strings

lupdate程序自动为每个源文本提供上下文。 此上下文是包含tr（）调用的类的类名。 在绝大多数情况下，这已足够。 但是，有时翻译人员需要更多信息来唯一标识源文本。 例如，一个对话框包含两个单独的框架，每个框架都包含一个“ Enabled”选项，因为在某些语言中两者之间的翻译会有所不同，因此每个对话框都需要标识。 使用tr（）调用的两个参数形式很容易实现这一点，例如

```c++
rbc = new QRadioButton(tr("Enabled", "Color frame"), this);
```

and

```c++
rbh = new QRadioButton(tr("Enabled", "Hue frame"), this);
```

**Ctrl键加速器也可以翻译**：

```c++
 exitAct = new QAction(tr("E&xit"), this);
 exitAct->setShortcut(tr("Ctrl+Q", "Quit"));
```

强烈建议将tr（）的两个参数形式用于Ctrl键加速器。 第二个参数是翻译器关于加速器执行功能的唯一线索。

### Helping the Translator with Navigation Information

在大型复杂的应用程序中，翻译人员可能很难查看特定源文本的来源。 这个问题可以通过使用关键字TRANSLATOR添加注释来解决，该注释描述了导航至相关文本的导航步骤； 例如

```c++
/*
     TRANSLATOR FindDialog

     Choose Edit|Find from the menu bar or press Ctrl+F to pop up the
     Find dialog.

     ...
 */
```

### Handling Plural Forms处理复数形式

Qt包含tr（）重载，这将使编写“可感知多个”国际化应用程序变得非常容易。 此重载具有以下特征：

```c++
QString tr(const char *text, const char *comment, int n);
```

根据n的值，tr（）函数将返回不同的翻译，以及目标语言的正确语法编号。 同样，％n的任何出现都将替换为n的值。 例如：

```c++
 tr("%n item(s) replaced", "", count);
```

如果加载了法语翻译，则将根据n的值扩展为“ 0项复制品”，“ 1项复制品”，“ 2项复制品”等。 并且如果未加载任何翻译，则使用原始字符串，其中％n替换为count的值（例如，“替换了6个项目”）。

要处理母语的复数形式，您还需要加载该语言的翻译文件。 lupdate具有-pluralonly命令行选项，该选项允许创建仅包含具有多种形式的条目的TS文件。

### Coping With C++ Namespaces应对C ++命名空间

C ++名称空间和using名称空间语句可能会使lupdate混淆。 即使MyClass是在MyNamespace命名空间中定义的，它也会将MyClass :: tr（）解释为含义，而不是MyNamespace :: MyClass :: tr（）。 因此，这些字符串的运行时转换将失败。

您可以通过在使用MyClass :: tr（）的源文件的开头放置一个TRANSLATOR注释来解决此限制：

```c++
 /*
     TRANSLATOR MyNamespace::MyClass

     Necessary for lupdate.

     ...
 */
```

注释之后，对MyClass :: tr（）的所有引用将被理解为MyNamespace :: MyClass :: tr（）的含义。

## 2.翻译QObject子类外部的文本

### 2.1.Using QCoreApplication::translate()

如果引用的文本不在QObject子类的成员函数中，请直接使用适当类的tr（）函数或QCoreApplication :: translate（）函数：

```c++
 void some_global_function(LoginWidget *logwid)
 {
     QLabel *label = new QLabel(
             LoginWidget::tr("Password:"), logwid);
 }

 void same_global_function(LoginWidget *logwid)
 {
     QLabel *label = new QLabel(
             qApp->translate("LoginWidget", "Password:"),
             logwid);
 }
```

### 2.2.Using QT_TR_NOOP() and QT_TRANSLATE_NOOP()

如果您需要在函数外部完全具有可翻译文本，则有两个宏可以帮助您：QT_TR_NOOP（）和QT_TRANSLATE_NOOP（）。 这些宏仅标记要由lupdate提取的文本。 宏扩展为仅文本（不带上下文）。

```c++
QString FriendlyConversation::greeting(int greet_type)
 {
     static const char* greeting_strings[] = {
         QT_TR_NOOP("Hello"),
         QT_TR_NOOP("Goodbye")
     };
     return tr(greeting_strings[greet_type]);
 }
```

Example of QT_TRANSLATE_NOOP():

```c++
static const char* greeting_strings[] = {
     QT_TRANSLATE_NOOP("FriendlyConversation", "Hello"),
     QT_TRANSLATE_NOOP("FriendlyConversation", "Goodbye")
 };

 QString FriendlyConversation::greeting(int greet_type)
 {
     return tr(greeting_strings[greet_type]);
 }

 QString global_greeting(int greet_type)
 {
     return qApp->translate("FriendlyConversation",
                             greeting_strings[greet_type]);
 }
```

