# QPluginLoader

继承关系：`QPluginLoader`->`QPluginLoader`

## 1.Properties

- fileName : QString

  此属性保存**插件的文件名**。

  要可加载，文件的后缀必须是根据平台的可加载库的有效后缀，例如 在Unix上为.so，在Mac OS X上为.dylib，在Windows上为.dll。 可以使用QLibrary :: isLibrary（）验证后缀。

  如果文件名不存在，将不会设置。 然后，此属性将包含一个空字符串。

  默认情况下，此属性包含一个空字符串。

  注意：在Symbian中，fileName必须指向插件存根文件。

- loadHints : QLibrary::LoadHints

  该属性保留**给load（）函数一些有关其行为方式的提示**。

  您可以提供有关**如何解析插件中符号的提示**。 默认情况下，未设置任何提示。

  有关此属性如何工作的完整说明，请参见QLibrary :: loadHints的文档。

## 2.Public Functions

- QPluginLoader ( QObject * parent = 0 )

- QPluginLoader ( const QString & fileName, QObject * parent = 0 )

- ~QPluginLoader ()

- QString	errorString () const

  返回带有最后发生的错误描述的文本字符串。

- QString	fileName () const

- QObject *	instance ()

  **返回插件的根组件对象**。 如果需要，将加载插件。 如果无法加载插件或无法实例化根组件对象，则该函数返回0。

  如果根组件对象被破坏，则调用此函数将创建一个新实例。

  销毁QPluginLoader时，不会删除此函数返回的根组件。 如果要确保删除根组件，则无需再访问核心组件时应立即调用unload（）。 最终卸载库后，根组件将自动删除。

  **组件对象是QObject。 使用qobject_cast（）访问您感兴趣的接口**。

- bool	isLoaded () const

- bool	load ()

  加载插件，如果插件加载成功，则返回true；否则返回false。 **由于instance（）始终在解析任何符号之前调用此函数，因此无需显式调用它**。 在某些情况下，您可能需要提前加载插件，在这种情况下，您将使用此功能。

- QLibrary::LoadHints	loadHints () const

- void	setFileName ( const QString & fileName )

- void	setLoadHints ( QLibrary::LoadHints loadHints )

- bool	unload ()

  卸载插件，如果可以卸载插件，则返回true； 否则返回false。

  这会**在应用程序终止时自动发生，因此您通常不需要调用此函数**。

  如果QPluginLoader的其他实例使用相同的插件，则调用将失败，并且仅当每个实例都调用了unload（）时才进行卸载。

  不要尝试删除根组件。 相反，依赖于该unload（）会在需要时自动将其删除。

## 3.Static Public Members

- QObjectList	staticInstances ()

  返回由插件加载器保存的静态插件实例（根组件）的列表。

## 4.Detailed Description

QPluginLoader类在运行时加载插件。

QPluginLoader提供对Qt插件的访问。 **Qt插件存储在共享库（DLL）中，与使用QLibrary访问的共享库相比，它们具有以下优点**：

- QPluginLoader检查插件是否与应用程序相同的Qt版本链接。
- QPluginLoader提供对根组件对象（instance（））的直接访问，而不是强迫您手动解析C函数。

**QPluginLoader对象的实例在单个共享库文件（称为插件）上运行**。它以独立于平台的方式提供对插件中功能的访问。要指定要加载的插件，请在构造函数中传递文件名，或使用setFileName（）进行设置。

最重要的功能是：load（）用于动态加载插件文件； isLoaded（）用于检查加载是否成功； instance（）用于访问插件中的根组件。如果尚未加载插件，instance（）函数将隐式尝试加载该插件。可以使用QPluginLoader的多个实例来访问同一物理插件。

**加载后，插件将保留在内存中**，直到所有QPluginLoader实例都已卸载，或者直到应用程序终止为止。您可以尝试使用unload（）卸载插件，但是如果QPluginLoader的其他实例使用相同的库，则调用将失败，并且仅当每个实例都调用了unload（）时，才进行卸载。在卸载发生之前，根组件也将被删除。

为了加快插件的加载和验证速度，加载过程中收集的某些信息将缓存在持久性内存中（通过QSettings）。例如，加载操作的结果（例如成功或失败）存储在缓存中，因此后续的加载操作不会尝试加载无效的插件。但是，如果插件的“上次修改时间”时间戳已更改，则插件的缓存条目将无效，并且无论缓存条目中的值如何，都将重新加载插件。然后，使用加载操作的新结果更新缓存条目。

这也意味着**每次更新插件或任何相关资源（例如共享库）时都必须更新时间戳，因为相关资源可能会影响加载插件的结果**。

有关如何使应用程序可通过插件扩展的更多信息，请参见如何创建Qt插件。

请注意，如果您的应用程序与Qt静态链接，则不能使用QPluginLoader。在这种情况下，您还必须静态链接到插件。如果需要在静态链接的应用程序中加载动态库，则可以使用QLibrary。

注意：在Symbian中，每当需要插件路径时，都必须使用插件存根文件。为了加载插件，可以将存根视为与实际插件二进制文件具有相同的名称。实际上，它们的扩展名是“ .qtplugin”而不是“ .dll”，但是此差异由QPluginLoader和QLibrary透明地处理，以避免在大多数Qt应用程序中需要Symbian特定的插件处理。需要插件存根，因为Symbian平台安全性拒绝所有对实际插件二进制文件所在目录的访问。