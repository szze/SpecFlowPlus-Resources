You can run your SpecFlow tests via SpecFlow+ Runner from the command line. Your specification project's directory contains a batch file, `runtests.cmd` that you can start to run your tests. You can also use `SpecRun.exe` located in the `..\packages\SpecRun.Runner.{version}\tools\` directory of your Visual Studio project to run your tests.

Start `SpecRun.exe` without any parameters to display an overview of the available commands. Use the `help` command to display information on a specific command, e.g. `SpecRun.exe help run`.

The following commands are available from the command line:

## run
Use `SpecRun.exe run` to run your tests using the following parameters:

|Parameter/option       |Required/optional|Description|
|-----------------------|-----------------|-----------|
|target                 |**Required**     |The assembly or test profile (`.srprofile` file) to be tested.|
|`/basefolder:`folder   |Assembly: **Required**<br><br>Profile: Optional         |Specifies the base folder for executing tests. All paths are relative to this path. <br>If you have specified an **assembly** as your `target`, you need to define the base folder as the path to the directory containing your assembly.<br>If you have specified a **test profile** (.srprofile) as your target, this overrides the `baseFolder` entry in your `.srprofile` file.|
|`/outputfolder:`folder |Optional         |Specifies the output folder for your logs and report file. All paths are relative to this path. If you have specified a test profile (.srprofile) as your target, this value overrides the `outputFolder` entry in your `.srprofile` file.<br>If no output folder is defined in your test profile, or your `target` is an assembly, the output folder defaults to the base folder if not specified from the command line.|
|`/log:`file            |Optional         |Specifies the target log file. This path is relative to your output folder.|
|`/report:`file         |Optional         |Specifies the target report file. This path is relative to your output folder.<br>**Note:** This option only affects the name of the report file defined in the &lt;Settings> section of your profile. It does not affect the reports defined in the &lt;Report> section; to change the name of the report file for these reports, use the `outputName` attribute instead.|
|`/filter:`filter        |Optional         |Applies a filter to your tests and only executes those that match your expression. This overrides the `filter` entry in your `.srprofile` file. An overview of the syntax can be found [here](Filter).|
|`/toolIntegration:`value|Optional        |Supported values: `None, VS2010, VS2012, VS2013, TeamCity, TFS`|
|`/debug`                |Optional        |Default: false |


**Example:**  
`SpecRun.exe run default.srprofile /basefolder:c:\MyProjectFolder /outputfolder:output /report:MyReport.html`  
Executes your tests using the `default.srprofile` file. The base folder is set to `C:\MyProjectFolder` while the output folder is set to `C:\MyProjectFolder\output` (the `output` folder is relative to the base folder). The generated report is output to `C:\MyProjectFolder\output\MyReport.html`.

## buildserverrun
Use `SpecRun.exe buildserverrun` to execute your tests in build server mode using the following parameters:

|Parameter/option       |Required/optional|Description|
|-----------------------|-----------------|-----------|
|target                 |**Required**     |The assembly or test profile (`.srprofile` file) to be tested.|
|`/basefolder:`folder   |Optional         |Specifies the base folder for executing tests. All paths are relative to this path. This overrides the `baseFolder` entry in your `.srprofile` file.|
|`/outputfolder:`folder |Optional         |Specifies the output folder for your logs and report file. All paths are relative to this path. This overrides the `outputFolder` entry in your `.srprofile` file.<br>**Note:** If you have not specified an output folder in your .srprofile, the output folder defaults to the base folder if not specified from the command line.|
|`/log:`file            |Optional         |Specifies the target log file. This path is relative to your output folder.|
|`/report:`file         |Optional         |Specifies the target report file. This path is relative to your output folder.|
|`filter:`filter        |Optional         |Applies a filter to your tests and only executes those that match your expression. This overrides the `filter` entry in your `.srprofile` file.|
|`/buildserver:`name     |Optional         |The build servers' product name (TFS, TeamCity) for specialised trace output.|

## register
Use `SpecRun.exe register` to register your SpecFlow+ license. You only need to register your license once per user per machine. The license is valid for all SpecFlow+ components.

|Parameter/option       |Required/optional|Description|
|-----------------------|-----------------|-----------|
|licenseKey             |**Required**     |The license key you received when you purchased SpecFlow+|
|issuedTo               |**Required**     |The name of the licensee. If you purchased your SpecFlow+ license online via SWREG, this is the email address you used to purchase the license. If you purchased SpecFlow+ directly from TechTalk, this is the value in the email you received containing your license information.<br>**Note:** If the name of the licensee contains spaces, enclose the value in quotation marks, e.g. `SpecRun.exe register IDK23032JASKWPCXMQL1IDPAKX== "John Smith"`.|

## unregister
Use `SpecRun.exe unregister` to unregister your SpecFlow+ license.


## about
Use `SpecRun.exe about` to display information such as your version number, build date and license information (licensee, upgrade until date/expiry date).

