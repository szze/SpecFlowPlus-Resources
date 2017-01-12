SpecFlow+ Runner profiles (`.srprofile` file extension) are XML files that determine how SpecFlow+ Runner executes your tests. This includes the behaviour when tests fail (e.g. repeat the test, abort after X failed tests), defining various target environments for your tests (e.g. different web browsers or x64/x86), enabling multi-threading, configuring folder and file paths and applying transformations to your default configuration file in order to change the transform the configuration file for different target environments. 

A file named `Default.srprofile` is automatically added to your Visual Studio project when you add the NuGet package to your solution. This profile is relatively basic, and includes your project name, ID and various default settings. It also includes a commented out section that you can use to transform the database connection string in your configuration file in order to access a different database instance. 

The name of the profile file used by your project is defined using the `<Profile>` tag in your `.runsettings` file.

#SpecFlow+ Runner Profile Elements and Attributes
The following XML elements and attributes are available:

<h2 id="TestProfile">&lt;TestProfile></h2>

The `<TestProfile>` element is a container for the remaining elements.

<h2 id="Settings">&lt;Settings> </h2>
The `<Settings>` element defines general settings for your project. The following attributes are available:

|Attribute     |Required/Optional|Description|
|--------------|-----------------|-----------|
|projectName   |**Required**     |Name of the project. The project name is entered automatically when adding the NuGet package to your project. The project name is used to generate the default name of your report or log files.|
|name          |Optional         |Name of the settings (optional). By default, this name is used to generate the name of your report or log files (but an alternative file name can be specified in your .runsettings file or from the [[command line|SpecFlowPlus-Runner-Command-Line]]).|
|projectID     |Optional         |The GUID of the project. Entered automatically when adding the NuGet package to your project.|
|baseFolder    |Optional         |The folder where SpecFlow+ searches for assemblies that contains the tests to execute <b>when running tests from the [[command line|SpecFlowPlus-Runner-Command-Line]]</b>. This is `\bin\*` by default. Other paths specified in the profile are relative to this path, e.g. the location of report templates (see below).<br><b>When running tests from within Visual Studio</b>, the folder containing the assembly  that is being tested is always used as the base folder.|
|outputFolder  |Optional         |Output folder for reports and log files, relative to the base folder, <b>when running tests from the command line</b>. The default path is the value of `baseFolder`.|
|reportTemplate|Optional         |The report template used to output the results of your tests (relative to the base folder).<br>**NOTE:** If you add this file to your VS project, you can set **Copy to Output Directory** to "Copy always" to ensure the file is always copied to the `\bin` directory when running your tests.<br>You can specify additional reports in the `<Report>` element if you want to output more than one report per test run.|
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

<h2 id="Server">&lt;Server> </h2>

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

<h2 id="Execution">&lt;Execution> </h2>

The `<Execution>` element defines how your tests are executed. The following attributes are available:

|Attribute         |Required/Optional|Description|
|------------------|-----------------|-----------|
|stopAfterFailures |Optional         |The number of failed tests after which the execution of all tests is stopped. Set this to 0 (zero) to execute all tests, irrespective of the number of failures. If not specified, this defaults to 10. **Note:** The value in the default `.srprofile` shipped with the NuGet package is 3.| 
|testSchedulingMode|Optional         |Determines the order in which SpecRun executes your tests:<br>`Sequential`: Tests are always executed in the same order (default). The order in which tests are executed is predictable and always the same, but cannot be influenced manually.<br>`Random`: The order of tests is randomised. This can be useful to detect flickering scenarios that may pass/fail depending on the order in which the other tests area executed.<br>`Adaptive`: SpecRun uses the statistics available in the pass/fail history to determine which tests to run first. Previously failing tests and new tests are executed before successful and stable tests.<br><b>Note:</b> If you set the `testSchedulingMode` to `Adaptive` when no previous test execution results are available (e.g. no server has been configured, or the server is unreachable), the tests are executed using the `Random` option instead.|
|testThreadCount  |Optional          |The number of tests threads used to execute tests (default=1). <br>While there is no maximum number of threads, setting this value too high can reduce performance as the individual threads compete for processing power. Setting the number of threads to one less that your number of cores is recommended for `Process` test thread isolation (`testThreadIsolation` setting). You can generally use higher numbers for isolation using `AppDomain` and `SharedAppDomains`.<br>**Note:** Just increasing the number of threads on its own may cause issues, e.g. if the threads access the same database. It thus makes sense to combine this with a relocation and transformation of the .config file using the `{TestThreadId}` placeholder in the name of the new file and database instances (see <DeploymentTransformation> below).|
|retryFor         |Optional          |Determines which tests should be retried based on their status. Available options:<br>`None`: No tests are retried<br>`Failing`: Failing test are retried (default)<br>`All`: All tests are retried, including those that pass<br>**Note:** Tests are retried immediately after returning the corresponding status and before any subsequent tests are executed.|
|retryCount       |Optional          |The number of times tests whose execution status matches the value defined in `<retryFor>` are retried (default = 2).| 
|apartmentState   |Optional          |Sets the apartment state used to execute the tests. Possible values:<br>`STA`: Single Threaded Apartment. Use this if your application is not thread-safe<br>`MTA`: Multi-Threaded Apartment<br>`Unknown`: The ApartmentState is not set (default); tests run in same thread as SpecFlow+|
     
<h2 id="Environment">&lt;Environment> </h2>

The `<Environment>` element defines your target platform environment. The following attributes are available:

|Attribute          |Required/Optional|Description|
|-------------------|-----------------|-----------|
|framework          |Optional         |The .NET framework in use. SpecFlow+ determines which CLR (Command Language Runtime) version to use to execute the tests based on this setting:<br>`Net35`: .NET 3.5 - CLR 2.0<br>`Net40`: .NET 4.0 - CLR 4.0<br>`Net45`: .NET 4.5 - CLR 4.0<br>`Default`: CLR 4.0 (default)|
|platform           |Optional         |The target platform architecture: x86, x64 or Default (the setting under **Test&#124;Test Settings&#124;Default Processor Architecture** in Visual Studio)|
|testThreadIsolation|Optional         |Determines the level of thread isolation. Possible values: `AppDomain` (default), `SharedAppDomain` (from version 1.4) or `Process`.|
|apartmentState     |Optional         |Sets the apartment state used to execute the tests. Possible values:<br>`STA`: Single Threaded Apartment. Use this if your application is not thread-safe<br>`MTA`: Multi-Threaded Apartment<br>`Unknown`: The ApartmentState is not set (default); tests run in same thread as SpecFlow+|

<h2 id="TestAssemblyPaths">&lt;TestAssemblyPaths> </h2>

The `<TestAssemblyPaths>` element is a container for `<TestAssemblyPath>` elements, which define your assembly paths when executing tests from the command line. Paths in `<TestAssemblyPath>` elements are relative to the base folder.

**Example:** 
```xml
<TestAssemblyPaths>
    <TestAssemblyPath>SpecRun.TestProject.dll</TestAssemblyPath>
</TestAssemblyPaths>
```

<h2 id="Filter">&lt;Filter> </h2>

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
<ul>
<li>|: OR</li>
<li>&amp;: AND (however you need to use <code>&amp;amp;</code> instead in the profile, as it is an XML file)</li>
<li>!: NOT</li>
</ul>

**Examples:**  
`<Filter>@MyTag &amp; @YourTag</Filter>` executes all tests with both the `@MyTag` and `@YourTag` tags.  
`<Filter>tagmatch:!Tag[1-9]</Filter>` executes all tests that are not tagged with any of  `@Tag1` to `@Tag9`.  
<`Filter>@MyTag | tagmatch:tag[1-9]</Filter>` executes all tests with either the `@MyTag` tag or tags `@Tag1` to `@Tag9`.

<h2 id="Targets">&lt;Targets> </h2>
 
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
      <Filter>@32bit</Filter>
      <Environment platform="x86" apartmentState="STA" testThreadIsolation="Process"/> 
   </Target> 
</Targets> 
```
<h2 id="DeploymentTransformation">&lt;DeploymentTransformation> </h2>

This element is used to define transformations that are applied to your configuration file. You can nest this element within a `<Target>` element, allowing you to define different configuration settings per target, e.g. for different platforms (x64/x86) or for different web browsers. You can also use `{Target}` as a placeholder for this value, in which case the placeholder is replaced with the target name. See the [[SeleniumWebTest sample project|https://github.com/techtalk/SpecFlow.Plus.Examples/tree/master/SeleniumWebTest]] for an example ofusing placeholders to transform a configuration file.

The following elements and attributes are available:

|Element/Attribute  |Required/Optional|Description|
|-------------------|-----------------|-----------|
|GlobalSteps        |Optional         |Deployment transformation steps that are applied globally. Global steps are only applied once.|
|Steps              |**Required**     |Deployment transformation steps for your configuration file.|
|CopyFolder         |Optional         |Copies a specific folder to the test run instance:<br>`source`: Source folder to copy<br>`target`: Target folder<br>`deleteFolderOnRestore`: Determines whether the folder is deleted if an error occurs during the test run (default=true).<br>**Example:** `<CopyFolder source="%TMP%\SpecRunTestSource" target="%TMP%\SpecRunTestCopy" />` |
|ConfigFileTransformation|Optional    |Defines the transformation applied to the configuration file.<br>`configFile`: the configuration file to transform (optional)<br>`Transformation:` The transformation applied to the file.|
|Relocate            |Optional        |Changes the location where the tests run, allowing you to continue developing while your tests run (as the `bin/debug` folder is no longer used to execute tests).<br>`targetFolder`: The folder the application is moved to for testing. Moving this to another folder than `/bin/debug` means you can continue working in Visual Studio while the tests run.<br>`deleteFolderOnRestore`: Determines whether the folder is deleted if an error occurs during the test run.|
|RelocateConfigurationFile|Optional    |Used to relocate the configuration file:<br>`target`: The target location of the relocated config file relative to the base folder<br>Relocating your configuration file creates a copy of the test assembly configuration file, allowing each thread to be configured differently. It makes sense to include the `{TestThreadId}` placeholder in the relocated file's name so that a different file is used by each thread. <br>**Note:** Any transformations applied to your default configuration file are also applied to the relocated files.| 
|Custom              |Optional         |You can write your own deployment steps that are executed. The corresponding class must implement `TechTalk.SpecRun.Framework.IDeploymentTransformationStep`.<br>Add a `<CustomStep>` element for each step containing the following attributes:<br>'Type': The type that implements the custom step, either the name of the corresponding class with its namespace, or the file name and the name of the corresponding class with its namespace.<br>`arguments`: The arguments used by the custom step. If this is a string, the string can be accessed via DeploymentContext.CustomData.|
|IISExpress          |Optioonal        |Used to test web applications. Atributes:<br>'webAppFolder': The path to the web application you want to test.<br>`iisExpressPath`: The path to IISExpress (default = `%ProgramFiles%\IIS Express\iisexpress.exe`).<br>`port`: The port used by IISExpress to listen for requests (default = 8080).<br>`useShellExecute`: Determines whether to start IISExpress with or without the shell.|

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

<h2 id="TestThreads">&lt;TestThreads> </h2>

The `<TestThreads>` element is a container for `<TestThread>` elements. The following attributes are available for `<TestThread>` elements: 


|Element/Attribute  |Required/Optional|Description|
|-------------------|-----------------|-----------|
|id               |     |Integer ID of the test thread (zero-indexed). This value can be accessed using the `{TestThreadId}` placholder. |
|TestAffinity       |Optional         | Defines a filter applied to tests run in this thread. Only tests containing with the specified tag are executed in the thread.<br>**Example:** `<TestAffinity>testpath:Target:FireFox</TestAffinity>` only executes tests with the `FireFox` tag in the thread.|

You can use the `{TestThreadId}` as a placeholder to reference the thread ID, e.g. to transform the name of the database instance you are accessing based on the thread ID, ensuring that each thread accesses a separate instance of the database. This prevents the threads from conflicting with one another when accessing the database, as thread 0 may manipulate data that is required by thread 1 otherwise.

<h2 id="Report">&lt;Report></h2>
|Attribute     |Required/Optional|Description|
|--------------|-----------------|-----------|
|disable       |Optional         |Set this attribute to true to disable the report generation (default: `false`)|
|copyAlsoToBaseFolder|Optional   |Set this to true to also copy all the generated reports to the base folder (default: `false`)|
|Template      |Optional         |Use this element to define the template(s) used to generate reports. You can specify any number of templates; a report will be generated using each template specified. The following attributes are available for this element:<br>`name`: The path to the template .cshtml file, relative to the base folder<br>`outputName`: The path of the generated report, relative to the base folder|

**Note:** The report template specified in the `<Settings>` element (`reportTemplate`) is used in addition to the templates specified in the `<Report>` element.

**Examples:**

To disable the report generation:

```xml
<TestProfile xmlns="http://www.specrun.com/schemas/2011/09/TestProfile">
    <Settings name="Disable Reports" projectName="SpecRun Test Project" />
    <Report disable="true"/>
    <TestAssemblyPaths>
        <TestAssemblyPath>SpecRun.TestProject.dll</TestAssemblyPath>
    </TestAssemblyPaths>
</TestProfile>
```
To output 2 additional reports and copy the reports to the base folder:

```xml
<TestProfile xmlns="http://www.specrun.com/schemas/2011/09/TestProfile">
    <Settings name="Multiple Reports" projectName="SpecRun Test Project" />
    <Report>
        <Template name="CustomReportTemplate_1.cshtml" outputName="Report1.html" copyAlsoToBaseFolder="true"/>
        <Template name="CustomReportTemplate_2.cshtml" outputName="Report2.html" copyAlsoToBaseFolder="true"/>
    </Report>
    <TestAssemblyPaths>
        <TestAssemblyPath>SpecRun.TestProject.dll</TestAssemblyPath>
    </TestAssemblyPaths>
</TestProfile>
```


<h2 id="Placeholders">Placeholders</h2>

There are placeholders available for the elements defined in your profile. You can use these placeholders in your configuration file. This allows you to use the same configuration file for various target environments, e.g. you could use the `{TestThreadId}` placeholder in the name of your database instance to ensure that each thread accesses a different instance of your database (Instance0, Instance1 etc.) . 

The following placeholders are available:

* `{TestThreadId}`: The ID of the current thread (integer)
* `{Target}`: The name of the current target (string)
* `{UniqueId}`: The unique ID entered in the profile
* `{BaseFolder}`: The base folder
* `{OutputFolder}`: The output folder for test results and reports
* All environment variables (specified using the standard format, i.e. enclosed in percentage signs ('%'))

Placeholders can be used in the following elements:

* ConfigFileTransformation/Transformation 
* CopyFile/target
* CopyFile/source 
* CopyFile/targetFolder
* CopyFolder/source 
* CopyFolder/target 
* CustomDeploystep/type (in the assembly path) 
* IISExpress/Port 
* IISExpress/webAppFolder 
* IISExpress/iisExpressPath 
* RelocateConfigurationFile/target 
* Relocate/targetFolder