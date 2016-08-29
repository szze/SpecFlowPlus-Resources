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

### Configuring SpecFlow to use your Template
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

## From Template to Report
The .cshtml Razor template determines the output of the final HTML report. The template can include both static HTML and dynamically generated content. You therefore have access to all the formatting options HTML provides, and you can use C# to dynamically determine the contents of the report.

If you open the default template or your renamed copy of it, you will notice it contains a series of helper functions, and an HTML section (starting from “<html>”). We will be extending both the helper functions to implement additional logic (e.g. to populate statistical charts) and the HTML to include additional information (e.g. embed the chart) in the output.

### Referencing Test Data from SpecFlow+
You can reference the [[properties|http://specflow.org/api/report/docs/]] by SpecFlow+ to perform calculations and output information on the test run you are interested in. Use the '@' character as a prefix to reference these properties, e.g. `@Model.Configuration.ProjectName` returns the name of your project. 

You can see this in action for yourself. Search for “&lt;body>” in your template to locate the start of the HTML report’s body:
```xml
<body>
        <h1>@Model.Configuration.ProjectName Test Execution Report</h1>
```
The second line defines the top level heading (h1 element) at the start of the report. [[@Model.Configuration.ProjectName|http://specflow.org/api/report/docs/class_tech_talk_1_1_spec_run_1_1_framework_1_1_configuration_1_1_test_profile_settings.html#a6c54a15903a60ea12189a42731ee2961]] accesses the name of your project while “Test Execution Report” is plain (static) text. As mentioned before, the ‘@’ character is used to denote code sections or variables to embed in your HTML.

Let's make a minor change to the report's heading:

1. Change “@Model.Configuration.ProjectName” to “[[@Model.Configuration.TestProfileSettings.ReportTemplate|http://specflow.org/api/report/docs/class_tech_talk_1_1_spec_run_1_1_framework_1_1_configuration_1_1_test_profile_settings.html#a25b29cff361f816a64c67800199c560e]]”
1. Change “Test Execution Report” to “is my new Test Execution Report template”.  
  The content should look like this:  
	&lt;body>  
        &lt;h1>@Model.Configuration.TestProfileSettings.ReportTemplate is my new Test Execution Report template&lt;/h1>  
2. Run your tests and click on the link to the report to view the output. The header should now be similar to the following:

XXX SCREENSHOT XXX

While this is a trivial example, it demonstrates how to integrate information passed by SpecFlow+ in your report and how to include it in the HTML output.
