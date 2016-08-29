**Note:** This tutorial assumes that you have already set up a Visual Studio project with SpecFlow+ Runner and have several tests that are executed. If you have not yet set up a project, refer to the [[Getting Started|http://www.specflow.org/getting-started]] guide first.

# Customising Reports
You can output HTML reports after each test execution run that include information on the tests in the test run, e.g. their status (passed/failed), the number of retries, execution time etc. SpecFlow+ Runner includes a default report template (`ReportTemplate.cshtml`) that you can use as the basis for customising your own reports. This tutorial will take you through the process of customising the default report template to include sortable lists, a graphical representation of statistical data and more.

The default template is located in the `\packages\[SpecRun.Runner]\templates` directory of your Visual Studio projects. **We recommend making a copy of this template, rather than editing it directly**.

## Initial Setup
The following initial steps are optional but highly recommended:  

1. Create a copy of the `ReportTemplate.cshtml` file in the `\packages\[SpecRun.Runner]\templates` directory of your VS project, and give this file a new name (e.g. `MyReportTemplate.cshtml`).
2. Add the template file to your specification project in Visual Studio so you can edit it directly in Visual Studio.
3. Set the template file’s **Copy to Output Directory** property to “Copy always” to ensure that the up-to-date template is available when executing your tests.
4. Add the necessary DLLs to your project as references to [[enable Intellisense|Reports#using-intellisense]].

XXX SCREENSHOT OF COPY ALWAYS? XXX

## Configuring SpecFlow to use your Template
Before you can use your new template, you need to tell SpecFlow+ Runner where to find the template. You can also determine the name of the HTML report file that is generated. To do so:

1. Open your project in Visual Studio.
1. Open your `.srprofile` file (the default name is `Default.srprofile`).
1. Edit the `Settings` element as required:
    1.	`projectName`: The name of your project and the first portion of the name of the report.
    1.	`name`: The name of your settings and the second portion of the report’s name.
    1.	`outputFolder`: The folder the report is output to, relative to your base folder (`baseFolder` attribute).
    1.	`reportTemplate`: The location of the report template used to generate the report, relative to your base folder. Enter the name of the template you created earlier here.
1. A time stamp (date in YYYY-MM-DD format ant time in HHMMSS format) is appended to the generated report. The final name of the generated report is composed as follows:
`<projectName>_<name>_YYYY-MM-DDTHHMMSS`
1. Run your tests and click on the link to the generated report in the **Output** window in Visual Studio to ensure that your report template can be located and a report is generated.

**Note:** You can generate multiple reports from the same test run. To generate additional reports, use the `<Report>` element as described [[here|SpecFlowPlus-Runner-Profiles#report]].