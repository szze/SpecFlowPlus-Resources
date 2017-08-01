The `<Environment>` element defines your target platform environment. The following attributes are available:

|Attribute          |Required/Optional|Description|
|-------------------|-----------------|-----------|
|framework          |Optional         |The .NET framework in use. SpecFlow+ determines which CLR (Command Language Runtime) version to use to execute the tests based on this setting:<br>`Net35`: .NET 3.5 - CLR 2.0<br>`Net40`: .NET 4.0 - CLR 4.0<br>`Net45`: .NET 4.5 - CLR 4.0<br>`Default`: CLR 4.0 (default)|
|platform           |Optional         |The target platform architecture: x86, x64 or Default (the setting under **Test&#124;Test Settings&#124;Default Processor Architecture** in Visual Studio)|
|testThreadIsolation|Optional         |Determines the level of thread isolation. Possible values: `AppDomain` (default), `SharedAppDomain` (from version 1.4) or `Process`.|
|apartmentState     |Optional         |Sets the apartment state used to execute the tests. Possible values:<br>`STA`: Single Threaded Apartment. Use this if your application is not thread-safe<br>`MTA`: Multi-Threaded Apartment<br>`Unknown`: The ApartmentState is not set (default); tests run in same thread as SpecFlow+|