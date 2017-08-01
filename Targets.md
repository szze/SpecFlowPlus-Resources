The `<Targets>` element is a container element for `<Target>` elements. Each `<Target>` element defines a test target. Tests are executed for each target, and you can define different target environments for your test. For example, you can define a target for x64 and x86 environments. You can also apply filters to each target, e.g. to only execute tests tagged with `@cloud` in browser environments. Tests that are executed for multiple targets are listed multiple times in the Test Explorer window, once for each target. See the [[SeleniumWebTest sample project|https://github.com/techtalk/SpecFlow.Plus.Examples/tree/master/SeleniumWebTest]] for an example of using different targets.  

The following attributes are available for the `<Target>` element:

|Attribute          |Required/Optional|Description|
|-------------------|-----------------|-----------|
|name               |**Required**     |Name of the target. This value can be accessed using the `{Target}` placeholder, e.g. when transforming your configuration file.|
|Filter             |Optional         |Filters the tests to execute by various attributes, such as tags or scenario. Boolean operators are supported and can be used to combine criteria. The following operators are supported:<br>!: NOT<br>&: AND<br>&#124;: OR<br>Regular expression can be used in filters, e.g. `tagmatch:tag\d` and `tagmatch:"ta(g)\d"`<br>**Note:** Tags and filters are case-sensitive.|
|Environment        |Optional         |`<Environment>` element containing the environment settings for the target, see [[&lt;Environment>|Environment]].|
|DeploymentTransformationSteps|Optional|Deployment transformation steps defined for the target, see [[&lt;DeploymentTransormation>|DeploymentTransformation]]. |

**Example:**
```xml
<Targets> 
   <Target name="32bit"> 
      <Filter>@32bit</Filter>
      <Environment platform="x86" apartmentState="STA" testThreadIsolation="Process"/> 
   </Target> 
</Targets> 
```