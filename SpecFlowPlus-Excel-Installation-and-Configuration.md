## Installation

The plugin can be installed from NuGet. 
```
Install-Package SpecFlow.Plus.Excel -ProjectName myproject
```

## Setup

If you install the package from NuGet, that the package should perform the necessary configuration steps. You can ensure that the SpecFlow+ Excel plugin is properly configured for SpecFlow in the `App.config` file:

```xml
<specFlow>
  <plugins>
    <add name="SpecFlow.Plus.Excel" type="Generator" />
  </plugins>
</specFlow>
```
