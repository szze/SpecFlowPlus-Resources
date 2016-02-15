SpecFlow+ Runner profiles (`.srprofile` file extension) are XML files that determine how SpecFlow+ Runner executes your tests. This includes the behaviour when tests fail (e.g. repeat the test, abort after X failed tests), defining various target environments for your tests (e.g. different web browsers or x64/x86), enabling multi-threading, configuring folder and file paths and applying transformations to your default configuration file in order to change the transform the configuration file for different target environments. 

A file named `Default.srprofile` is automatically added to your Visual Studio project when you add the NuGet package to your solution. This profile is relatively basic, and includes your project name, ID and various default settings. It also includes a commented out section that you can use to transform the database connection string in your configuration file in order to access a different database instance. 

The name of the profile file used by your project is defined using the `<Profile>` tag in your `.runsettings` file.

#SpecFlow+ Runner Profile Elements and Attributes
The following XML elements and attributes are available:

## &lt;TestProfile>
The `<TestProfile>` element is a container for the remaining elements.

## &lt;Settings> 
The `<Settings>` element defines general settings for your project. The following attributes are available:

|Attribute     |Required/Optional|Description|
|--------------|-----------------|-----------|
|projectName   |**Required**     |Name of the project. The project name is entered automatically when adding the NuGet package to your project. The project name is used to generate the default name of your report or log files.|
|name          |Optional         |Name of the settings (optional). By default, this name is used to generate the name of your report or log files (but an alternative file name can be specified in your .runsettings file or from the [[command line|SpecFlowPlus-Runner-Command-Line]]).|
|projectID     |Optional         |The GUID of the project. Entered automatically when adding the NuGet package to your project.|
|baseFolder    |Optional         |The folder where SpecFlow+ searches for assemblies that contains the tests to execute when running tests from the [[command line|SpecFlowPlus-Runner-Command-Line]]. This is `\bin\*` by default. Other paths specified in the profile are relative to this path, e.g. the location of report templates (see below).|
|outputFolder  |Optional         |Output folder for reports and log files, relative to the base folder, when running tests from the command line. The default path is the value of `baseFolder`.|
|reportTemplate|Optional         |The report template used to output the results of your tests (relative to the base folder).<br>**NOTE:** If you add this file to your VS project, you can set **Copy to Output Directory** to "Copy always" to ensure the file is always copied to the `\bin` directory when running your tests.|
|licenseKey    |Optional         |Location of the license key for project or OEM licenses.|

**Example:**  
```xml
<Settings
    name="MySettings"
    projectName="MyProject"
    projectId="{7B359152-D36D-4D5A-BFDB-ED78B094D619}"
    baseFolder="C:\MyBaseFolder"
    outputFolder="..\OutputFolder"
    reportTemplate="MyTemplate.cshtml"/>
```

## &lt;Server> 
You can publish the results of your tests to a SpecFlow+ Runner server. Details on setting up the server can be found [[here|Setting-up-the-SpecFlowPlus-Runner-Server]].

The following attributes are available:

|Attribute     |Required/Optional|Description|
|--------------|-----------------|-----------|
|serverURL     |**Required**     |The full URL of the SpecFlow+ Runner server, including transfer protocol and port number (6365)|
|publishResults|Optional         |Determines whether the results are published to the server or not (default = false) 

**Example:**  
```xml
<Server serverUrl="http://specrun.server:6365" publishResults="true" />
```

## &lt;Execution> 
The `<Execution>` element defines how your tests are executed. The following attributes are available:

|Attribute         |Required/Optional|Description|
|------------------|-----------------|-----------|
|stopAfterFailures |Optional         |The number of failed tests after which the execution of all tests is stopped. Set this to 0 (zero) to execute all tests, irrespective of the number of failures. If not specified, this defaults to 10. **Note:** The value in the default `.srprofile` shipped with the NuGet package is 3.| 
|testSchedulingMode|Optional         |Determines the order in which SpecRun executes your tests:<br>`Sequential`: Tests are always executed in the same order (default). The order in which tests are executed is predictable and always the same, but cannot be influenced manually.<br>`Random`: The order of tests is randomised. This can be useful to detect flickering scenarios that may pass/fail depending on the order in which the other tests area executed.<br>`Adaptive`: SpecRun uses the statistics available in the pass/fail history to determine which tests to run first. Previously failing tests and new tests are executed before successful and stable tests.|
|testThreadCount  |Optional          |The number of tests threads used to execute tests (default=1).<br>**Note:** Just increasing the number of threads may cause issues, e.g. if the threads access the same database. It thus makes sense to combine this with a relocation and transformation of the .config file using the `{TestThreadId}` placeholder in the name of the new file and database instances (see <DeploymentTransformation> below).|
|retryFor         |Optional          |Determines which tests should be retried based on their status. Available options:<br>`None`: No tests are retried<br>`Failing`: Failing test are retried (default)<br>`All`: All tests are retried, including those that pass|
|retryCount       |Optional          |The number of times tests whose execution status matches the value defined in `<retryFor>` are retried (default = 2).| 
|apartmentState   |Optional          |Sets the apartment state used to execute the tests. Possible values:<br>`STA`: Single Threaded Apartment. Use this if your application is not thread-safe<br>`MTA`: Multi-Threaded Apartment<br>`Unknown`: The ApartmentState is not set (default); tests run in same thread as SpecFlow+|
     
## &lt;Environment> 
The `<Environment>` element defines your target platform environment. The following attributes are available:

|Attribute          |Required/Optional|Description|
|-------------------|-----------------|-----------|
|framework          |Optional         |The .NET framework in use. SpecFlow+ determines which CLR (Command Language Runtime) version to use to execute the tests based on this setting:<br>`Net35`: .NET 3.5 - CLR 2.0<br>`Net40`: .NET 4.0 - CLR 4.0<br>`Net45`: .NET 4.5 - CLR 4.0<br>`Default`: CLR 4.0 (default)|
|platform           |Optional         |The target platform architecture: x86, x64 or Default (the setting under **Test&#124;Test Settings&#124;Default Processor Architecture** in Visual Studio)|
|testThreadIsolation|Optional         |Determines the level of thread isolation. Possible values: `AppDomain` (default) or `Process`.|
|apartmentState     |Optional         |Sets the apartment state used to execute the tests. Possible values:<br>`STA`: Single Threaded Apartment. Use this if your application is not thread-safe<br>`MTA`: Multi-Threaded Apartment<br>`Unknown`: The ApartmentState is not set (default); tests run in same thread as SpecFlow+|

## &lt;TestAssemblyPaths> 
The `<TestAssemblyPaths>` element is a container for `<TestAssemblyPath>` elements, which define your assembly paths when executing tests from the command line. Paths in `<TestAssemblyPath>` elements are relative to the base folder.

**Example:** 
```xml
<TestAssemblyPaths>
    <TestAssemblyPath>SpecRun.TestProject.dll</TestAssemblyPath>
</TestAssemblyPaths>
```

## &lt;Filter>
The `<Filter>` element allows you to define filters that are applied to your tests, allowing you to determine which tests to execute. Filters can also be defined in `<Target>` elements, in which case the filter only applies to that target. Filters defined outside of a `<Target>` element are applied globally. The **Test Explorer** window in Visual Studio only lists those tests that meet your filter criteria (after rebuilding your project). Note that global filters also apply when running tests by right-clicking on a feature file and selecting **Run SpecFlow Scenarios**.

Filters can be applied to tests based on tags (including regular expressions), or the scenario or feature name.

**Note:** Tags and filters are **case-sensitive**.

The following filter types can be defined:

|Prefix    |Type      |Description|
|----------|----------|-----------|
|@         |Tag       |Matches a tag exactly, e.g. '@MyTag' only returns those tests with the '@MyTag' tag.|
|tagmatch: |Tag       |Matches tags by regular expression, e.g. 'tagmatch:Tag[1-3]' matches tests with the tags 'Tag1', "Tag2' or 'Tag3'.|
|testpath:Feature: |Test      |Matches tests by feature name. You can use the `*` wildcard in feature names, e.g. `testpath:"Feature:Calcu*" matches the features "Calculator" and "Calculus".|
|testpath:Scenario:|Test      |Matches tests by scenario name. You can use the `*` wildcard in scenario names, e.g. `testpath:"Scenario:* two numbers" matches the scenarios "Add two numbers", "Subtract two numbers" and "Multiply two numbers".|

You can combine filters using logical operators. The following operators are supported:
* |: OR
* &: AND (however you need to use `&amp;` instead in the profile, as it is an XML file)
* !: NOT

**Examples:**  
`<Filter>@MyTag &amp; @YourTag</Filter>` executes all tests with both the `@MyTag` and `@YourTag` tags.  
`<Filter>tagmatch:!Tag[1-9]</Filter>` executes all tests that are not tagged with any of  `@Tag1` to `@Tag9`.  
<`Filter>@MyTag | tagmatch:tag[1-9]</Filter>` executes all tests with either the `@MyTag` tag or tags `@Tag1` to `@Tag9`.

## &lt;Targets> 
The `<Targets>` element is a container element for `<Target>` elements. Each `<Target>` element defines a test target. Tests are executed for each target, and you can define different target environments for your test. For example, you can define a target for x64 and x86 environments. You can also apply filters to each target, e.g. to only execute tests tagged with `@cloud` in browser environments. Tests that are executed for multiple targets are listed multiple times in the Test Explorer window, once for each target. 

The following attributes are available for the `<Target>` element:

|Attribute          |Required/Optional|Description|
|-------------------|-----------------|-----------|
|name               |**Required**     |Name of the target. This value can be accessed using the `{Target}` placeholder, e.g. when transforming your configuration file.|
|Filter             |Optional         |Filters the tests to execute by various attributes, such as tags or scenario. Boolean operators are supported and can be used to combine criteria. The following operators are supported:<br>!: NOT<br>&: AND<br>&#124;: OR<br>Regular expression can be used in filters, e.g. `tagmatch:tag\d` and `tagmatch:"ta(g)\d"`<br>**Note:** Tags and filters are case-sensitive.|
|Environment        |Optional         |`<Environment>` element containing the environment settings for the target, see <Environment> above.|
|DeploymentTransformationSteps|Optional|Deployment transformation steps defined for the target, see <DeploymentTransormation>below. |

**Example:**
```xml
<Targets> 
   <Target name="32bit"> 
      <Environment platform="x86" apartmentState="STA" testThreadIsolation="Process"/> 
   </Target> 
</Targets> 
```

### &lt;DeploymentTransformation> 
This element is used to define transformations that are applied to your configuration file. You can nest this element within a `<Target>` element, allowing you to define different configuration settings per target, e.g. for different platforms (x64/x86) or for different web browsers. You can also use `{Target}` as a placeholder for this value, in which case the placeholder is replaced with the target name.  

The following elements and attributes are available:

|Element/Attribute  |Required/Optional|Description|
|-------------------|-----------------|-----------|
|GlobalSteps        |Optional         |Deployment transformation steps that are applied globally. Global steps are only applied once.|
|Steps              |**Required**     |Deployment transformation steps for your configuration file.|
|CopyFolder         |Optional         |Copies a specific folder to the test run instance:<br>`source`: Source folder to copy<br>`target`: Target folder<br>`deleteFolderOnRestore`: Determines whether the folder is deleted before being copied if it already exists (default=true).<br>**Example:** `<CopyFolder source="%TMP%\SpecRunTestSource" target="%TMP%\SpecRunTestCopy" />` |
|ConfigFileTransformation|Optional    |Defines the transformation applied to the configuration file.<br>`configFile`: the configuration file to transform (optional)<br>`Transformation:` The transformation applied to the file.|
|Relocate            |Optional        |Changes the location where the tests run, allowing you to continue developing while your tests run (as the `bin/debug` folder is no longer used to execute tests).<br>`targetFolder`: The folder the application is moved to for testing. Moving this to another folder than `/bin/debug` means you can continue working in Visual Studio while the tests run.<br>`deleteFolderOnRestore`: Determines whether the folder is deleted before being copied if it exists.|
|RelocateConfigurationFile|Optional    |Used to relocate the configuration file:<br>`target`: The target location of the relocated config file relative to the base folder<br>Relocating your configuration file creates a copy of the test assembly configuration file, allowing each thread to be configured differently. It makes sense to include the `{TestThreadId}` placeholder in the relocated file's name so that a different file is used by each thread. <br>**Note:** Any transformations applied to your default configuration file are also applied to the relocated files.| 

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

## &lt;TestThreads> 
The `<TestThreads>` element is a container for `<TestThread>` elements. The following attributes are available for `<TestThread>` elements: 


|Element/Attribute  |Required/Optional|Description|
|-------------------|-----------------|-----------|
|name               |     |Integer ID of the test thread (zero-indexed). This value can be accessed using the `{TestThreadId}` placholder. |
|TestAffinity       |Optional         | Defines a filter applied to tests run in this thread. Only tests containing with the specified tag are executed in the thread.<br>**Example:** `<TestAffinity>testpath:Target:FireFox</TestAffinity>` only executes tests with the `FireFox` tag in the thread.|

You can use the `{TestThreadId}` as a placeholder to reference the thread ID, e.g. to transform the name of the database instance you are accessing based on the thread ID, ensuring that each thread accesses a separate instance of the database. This prevents the threads from conflicting with one another when accessing the database, as thread 0 may manipulate data that is required by thread 1 otherwise.


##Placeholders 
There are placeholders available for the elements defined in your profile. You can use these placeholders in your configuration file. This allows you to use the same configuration file for various target environments, e.g. you could use the `{TestThreadId}` placeholder in the name of your database instance to ensure that each thread accesses a different instance of your database (Instance0, Instance1 etc.) . 

The following placeholders are available:

* `{TestThreadId}`: The ID of the current thread (integer)
* `{Target}`: The name of the current target (string)