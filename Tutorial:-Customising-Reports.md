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

While this is a trivial example, it demonstrates how to integrate information passed by SpecFlow+ in your report and how to include it in the HTML output. The examples below include some more interesting customisations that you can use as the basis for your own templates.

#Examples
The following examples are intended to get you started and give you some ideas for how to customise your own reports.

##Screenshots
A common requirement is to include screenshots in the report to document errors. 
XXX INCOMPLETE XXX

##Sortable Lists
By default, the tables in the report are static and the columns cannot be sorted. However you can easily make your tables sortable using JavaScript. This can be particularly useful for sorting tests by execution time, for example, in order to determine which tests take a long time to execute and may therefore require optimisation.

For simplicity’s sake, this tutorial uses [[SortTable|http://www.kryogenix.org/code/browser/sorttable/]] by Stuart Langridge to create tables whose columns can be sorted by clicking in the column header. Download the source JavaScript file (sortable.js) from Stuart’s website at the previous link. Obviously you can use an alternative solution or roll your own – the principle is the same.

###Editing the Template
Once you have downloaded the JavaScript source, open your CSHTML template file and add a reference to the script to the start of the template:

```
@inherits TechTalk.SpecRun.Framework.Reporting.CustomTemplateBase<TestRunResult>
<!DOCTYPE html>
@using System
@using System.Linq
@using System.Globalization
@using TechTalk.SpecRun.Framework
@using TechTalk.SpecRun.Framework.Results
@using TechTalk.SpecRun.Framework.TestSuiteStructure
<script src="sorttable.js"></script>
```

###Adding a Sortable Table
Defining a sortable table using sortable.js is easy: just start your HTML table declaration with the following element:  
`<table class="sortable">`

The remaining definition of the table is standard HTML using <tr> and <td> elements. We will also need to define an “Index” column to ensure that we can revert the table to the default sort order at any time. The following code initialises the index to 0 (you can obviously start counting from 1 if you prefer) and defines the column headers for each of the columns for our test results:

```
int Index = 0;
<table class="sortable">
<tr>
    <th>Index</th>
    <th>Steps</th>
    <th>Trace</th>
    <th>Result</th>
    <th>Test duration</th>
</tr>
```

To populate the table with data, we are going to iterate through all the trace events returned by SpecFlow, ignoring any that are irrelevant:

```
@foreach (var traceEvent in test.Result.TraceEvents)
{ 
    if (!IsRelevant(traceEvent))
    {
        continue;
    }
```

… and add a row to the table for each relevant entry, with each column’s contents matching the header …

```
<tr>
    <td>@Index</td>
    <td>
        <pre class="log">@(traceEvent.BusinessMessages.TrimEnd())</pre>
    </td>
    <td>
                    <!-- [@traceEvent.Type: @relatedNode.Type - @relatedNode.Title] -->
                    <!-- Deleted due to errors -->

    </td>
    <td>@traceEvent.ResultType</td>
    <td>@GetSeconds(Math.Round(traceEvent.Duration.TotalSeconds, 3))s</td>
</tr>
```

XXX CHECK ERRORS IN CODE XXX

Finally, we need to increment the Index by one before looping through the next entry:
```
    Index = Index +1;
}
</table>
```

### Final Steps
While you can now run your tests and generate the report, you still need to ensure that the HTML output can access `sorttable.js`. For now, the just copy the file to your report’s output directory. In a real-life scenario you will probably want to ensure that this file is automatically deployed to this directory whenever you run your tests.

### The Final Output

XXX EMBED HTML XXX

