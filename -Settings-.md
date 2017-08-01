The `<Settings>` element defines general settings for your project. The following attributes are available:

|Attribute     |Required/Optional|Description|
|--------------|-----------------|-----------|
|projectName   |**Required**     |Name of the project. The project name is entered automatically when adding the NuGet package to your project. The project name is used to generate the default name of your report or log files.|
|name          |Optional         |Name of the settings (optional). By default, this name is used to generate the name of your report or log files (but an alternative file name can be specified in your .runsettings file or from the [[command line|SpecFlowPlus-Runner-Command-Line]]).|
|projectID     |Optional         |The GUID of the project. Entered automatically when adding the NuGet package to your project.|
|baseFolder    |Optional         |The folder where SpecFlow+ searches for assemblies that contains the tests to execute <b>when running tests from the [[command line|SpecFlowPlus-Runner-Command-Line]]</b>. This is `\bin\*` by default. Other paths specified in the profile are relative to this path, e.g. the location of report templates (see below).<br><b>When running tests from within Visual Studio</b>, the folder containing the assembly  that is being tested is always used as the base folder.|
|outputFolder  |Optional         |Output folder for reports and log files, relative to the base folder, <b>when running tests from the command line</b>. The default path is the value of `baseFolder`.|
|reportTemplate|Optional         |The report template used to output the results of your tests (relative to the base folder). If you add this file to your VS project, you can set **Copy to Output Directory** to "Copy always" to ensure the file is always copied to the `\bin` directory when running your tests.<br>**NOTE:** This setting is a legacy option that has been retained for compatibility. We recommend that you specify your report templates using the `<Report>` element instead. This also allows you to define more than one report per test run.|
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
