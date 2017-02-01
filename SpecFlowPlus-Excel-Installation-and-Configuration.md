## Installation

The SpecFlow+ Excel plugin is available from [NuGet](http://www.nuget.org/packages/SpecFlow.Plus.Excel). 

To add the package to your Visual Studio project:  
1. Right-click on your specification project and select **Manage Nuget Packages for Solution**.  
2. Search for "SpecFlow Excel" on nuget.org and install the SpecFlow+ Excel plugin

Alternatively, you can install the package from the NuGet console (**Tools | NuGet Package Manager | Package Manager Console**) as follows:
```
Install-Package SpecFlow.Plus.Excel -ProjectName myproject
```

## Setup

When installing the NuGet package, the necessary configuration steps are performed. You can verify that the SpecFlow+ Excel plugin is configured correctly for SpecFlow in the `App.config` file, which should contain the following section:

```xml
<specFlow>
  <plugins>
    <add name="SpecFlow.Plus.Excel" type="Generator" />
  </plugins>
</specFlow>
```
