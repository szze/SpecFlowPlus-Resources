This element is used to define transformations that are applied to your configuration file. You can nest this element within a `<Target>` element, allowing you to define different configuration settings per target, e.g. for different platforms (x64/x86) or for different web browsers. You can also use `{Target}` as a placeholder for this value, in which case the placeholder is replaced with the target name. See the [[SeleniumWebTest sample project|https://github.com/techtalk/SpecFlow.Plus.Examples/tree/master/SeleniumWebTest]] for an example of using placeholders to transform a configuration file.

The following elements and attributes are available:

|Element/Attribute  |Required/Optional|Description|
|-------------------|-----------------|-----------|
|GlobalSteps        |Optional         |Deployment transformation steps that are applied globally. Global steps are only applied once.|
|Steps              |**Required**     |Deployment transformation steps for your configuration file.|
|CopyFolder         |Optional         |Copies a specific folder to the test run instance:<br>`source`: Source folder to copy<br>`target`: Target folder<br>`deleteFolderOnRestore`: Determines whether the folder is deleted if an error occurs during the test run (default=true).<br>**Example:** `<CopyFolder source="%TMP%\SpecRunTestSource" target="%TMP%\SpecRunTestCopy" />` |
|ConfigFileTransformation|Optional    |Defines the transformation applied to the configuration file.<br>`configFile`: the configuration file to transform (optional)<br>`Transformation:` The transformation applied to the file.|
|Relocate            |Optional        |Changes the location where the tests run, allowing you to continue developing while your tests run (as the `bin/debug` folder is no longer used to execute tests).<br>`targetFolder`: The folder the application is moved to for testing. Moving this to another folder than `/bin/debug` means you can continue working in Visual Studio while the tests run.<br>`deleteFolderOnRestore`: Determines whether the folder is deleted if an error occurs during the test run.|
|RelocateConfigurationFile|Optional    |Used to relocate the configuration file:<br>`target`: The target location of the relocated config file relative to the base folder<br>Relocating your configuration file creates a copy of the test assembly configuration file, allowing each thread to be configured differently. It makes sense to include the `{TestThreadId}` placeholder in the relocated file's name so that a different file is used by each thread. <br>**Note:** Any transformations applied to your default configuration file are also applied to the relocated files.| 
|Custom              |Optional         |You can write your own deployment steps that are executed. The corresponding class must implement `TechTalk.SpecRun.Framework.IDeploymentTransformationStep`.<br>Add a `<Custom>` element for each step containing the following attributes:<br>`type`: The type that implements the custom step in the format `Path, DLL`, where `Path` includes the namespace and corresponding class (e.g. `DeploymentSteps.MySteps`) and where `DLL` is the name of the assembly containing the class.<br>`arguments`: The arguments used by the custom step. If this is a string, the string can be accessed via DeploymentContext.CustomData.|
|IISExpress          |Optional        |Used to test web applications. Atributes:<br>'webAppFolder': The path to the web application you want to test.<br>`iisExpressPath`: The path to IISExpress (default = `%ProgramFiles%\IIS Express\iisexpress.exe`).<br>`port`: The port used by IISExpress to listen for requests (default = 8080).<br>`useShellExecute`: Determines whether to start IISExpress with or without the shell.|

**Example:**
```xml
<DeploymentTransformation> 
   <Steps> 
      <ConfigFileTransformation configFile="App.config"> 
         <Transformation> 
            <![CDATA[<?xml version="1.0" encoding="utf-8"?> 
               <configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform"> 
                  <appSettings> 
                     <add key="foo" value="bar" xdt:Locator="Match(key)" xdt:Transform="Insert"/> 
                  </appSettings> 
               </configuration> 
            ]]> 
         </Transformation> 
      </ConfigFileTransformation> 
   </Steps> 
</DeploymentTransformation>
```
