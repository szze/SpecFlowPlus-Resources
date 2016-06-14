SpecFlow can generates reports once your tests have finished executing that include a breakdown of the results of your tests. The default report includes a statistical overview of the status of all tests, as well as information on individual scenarios, including Gherkin test cases, statistics on the total number and percentage of successful tests, and the execution time for each step. When running tests from within Visual Studio, a link to the generated report(s) is included in the **Output** window once the tests have completed.

The report is output to your output folder (configured in your [[profile|SpecFlowPlus-Runner-Profiles]]) and the name of the report is generated using the `projectName` and `name` defined in your profile plus a time stamp:
`<projectName>_<name>_YYYY-MM-DDTHHMMSS`

If you want to generate multiple reports from a single test run, you also need to modify your profile to include the templates and output paths for these reports. The settings for multiple reports are defined in the [[&lt;Report> element|SpecFlowPlus-Runner-Profiles#report]].

A Razor template is used to generate the reports, and the SpecFlow+ Runner NuGet package includes a default report template named ` ReportTemplate.cshtml` located in the `\packages\[SpecRun.Runner]\templates` directory of your Visual Studio project. You can customise this template to meet your needs. If you customise the template, we recommend renaming the template file as well. The data available to your reports is accessible using SpecFlow+'s report API. If you edit the .cshtml template in Visual Studio, Intellisense will display a short description of the available properties and methods. You can also reference them in the [[online report API documentation|http://www.specflow.org/api/report/docs/]].

## Defining Your Own Template

Please review the [SpecFlow+ Runner Report API Documentation](http://www.specflow.org/api/report/docs/) to find out about the classes and properties of the reporting model that can be referred in the reporting template.

To define your own report template:

1. Create a copy of `ReportTemplate.cshtml` (in `\packages\[SpecRun.Runner]\templates`) and rename it accordingly.
1. If desired, add the .cshtml file to your Visual Studio project so that you can edit in Visual Studio. If you do this, ensure that **Copy to Output Directory** in the file's properties is set to "Copy always" to ensure that the latest version of the template is always used to generate reports.
1. Edit your `.srprofile` file and change the value of the `reportTemplate` attribute in the `Settings` element to the name of your template file. This path is relative to your base folder (default: `\bin\`).
1. Change the `name` and `projectName` attributes in the `Settings` element to reflect your project. These values are used to name the generated report.
1. Execute your tests to generate the report.

## Using Intellisense
If you edit the template `.cshtml` file in Visual Studio, you can use Intellisense to access the properties and methods exposed by the API. To use Intellisense, reference the following DLLs from your project in VS:

* RazorEngine.dll
* System.Web.Razor.dll
* TechTalk.SpecRun.Framework.dll
* TechTalk.SpecRun.Framework.Interfaces.dll

These files are all included in the SpecFlow+ Runner NuGet package and are located in the `\packages\[SpecRun.Runner]` directory once you have added the NuGet package to your solution.
If you are using Resharper, referencing the DLLs is all that is necessary. If you care not using ReSharper, you will also need to follow the steps outlined [[here| http://thetoeb.de/2014/01/05/enabling-mvc5-intellisense-in-a-classlibrary-project/]].

## Generating a Single Report for Multiple Specification Projects
A SpecFlow+ report is generated for the `.srprofile` file used to execute the tests from the command line. You can add multiple assemblies to your `.srprofile` file, in which case the report will combine the results of the assemblies in a single report.

To generate a single report for multiple assemblies:  

1. Open the profile you want to edit and locate the `<TestAssemblyPaths>` section. This should already contain the path to the assembly linked to the project the profile belongs to.  
1. Add the test assemblies you want to include in the report as <TestAssemblyPath> elements. You need to specify the paths as relative to the location of the assembly associated with the profile's project. If all your projects are located in the same root folder, the path should be `../../../<ProjectDirectory>/bin/debug/<ProjectSpecificationAssembly>.dll`.  
1. Start `runtests.cmd` located in the directory of your edited profile. Your tests are executed and the report is generated.  

## Generating Multiple Reports in a Single Test Run
