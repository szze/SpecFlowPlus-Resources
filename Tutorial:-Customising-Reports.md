**Note:** This tutorial assumes that you have already set up a Visual Studio project with SpecFlow+ Runner and have several tests that are executed. If you have not yet set up a project, refer to the [[Getting Started|http://www.specflow.org/getting-started]] guide first.

This section also includes a couple of [[examples|https://github.com/techtalk/SpecFlowPlus-Resources/wiki/Tutorial:-Customising-Reports#examples]] of customising reports.

# Customising Reports
You can output HTML reports after each test execution run that include information on the tests in the test run, e.g. their status (passed/failed), the number of retries, execution time etc. SpecFlow+ Runner includes a default report template (`ReportTemplate.cshtml`) that you can use as the basis for customising your own reports. This tutorial will take you through the process of customising the default report template to include sortable lists, a graphical representation of statistical data and more.

The default template (`ReportTemplate.cshtml`) is located in the `\packages\[SpecRun.Runner]\templates` directory of your Visual Studio projects. **We recommend making a copy of this template, rather than editing it directly**.

## Initial Setup
The following initial steps are optional but highly recommended:  

1. Create a copy of the `ReportTemplate.cshtml` file in the `\packages\[SpecRun.Runner]\templates` directory of your VS project, and give this file a new name (e.g. `MyReportTemplate.cshtml`).
2. Add the template file to your specification project in Visual Studio so you can edit it directly in Visual Studio.
3. Set the template file’s **Copy to Output Directory** property to “Copy always” to ensure that the up-to-date template is available when executing your tests.
4. Add the necessary DLLs to your project as references to [[enable Intellisense|Reports#using-intellisense]].

### Configuring SpecFlow to use your Template
Before you can use your new template, you need to tell SpecFlow+ Runner where to find the template. You can also determine the name of the HTML report file that is generated. To do so:

1. Open your project in Visual Studio.
1. Open your `.srprofile` file (the default name is `Default.srprofile`).
1. Edit the `Settings` [[element|https://github.com/techtalk/SpecFlowPlus-Resources/wiki/SpecFlowPlus-Runner-Profiles#settings-]] as required:
    1.	`projectName`: The name of your project and the first portion of the name of the report.
    1.	`name`: The name of your settings and the second portion of the report’s name.
    1.	`outputFolder`: The folder the report is output to, relative to your base folder (`baseFolder` attribute).
    1.	`reportTemplate`: The location of the report template used to generate the report, relative to your base folder. Enter the name of the template you created earlier here.
1. A time stamp (date in YYYY-MM-DD format and time in HHMMSS format) is appended to the generated report. The final name of the generated report is composed as follows:
`<projectName>_<name>_YYYY-MM-DDTHHMMSS`
1. Run your tests and click on the link to the generated report in the **Output** window in Visual Studio to ensure that your report template can be located and a report is generated.

**Note:** You can generate multiple reports from the same test run. To generate additional reports, use the `<Report>` element as described [[here|SpecFlowPlus-Runner-Profiles#report]].

## From Template to Report
The .cshtml Razor template determines the output of the final HTML report. The template can include both static HTML and dynamically generated content. You therefore have access to all the formatting options HTML provides, and you can use C# to dynamically determine the contents of the report.

If you open the default template or your renamed copy of it, you will notice it contains a series of helper functions, and an HTML section (starting from `<html>`). We will be extending both the helper functions to implement additional logic (e.g. to populate statistical charts) and the HTML to include additional information (e.g. embed the chart) in the output.

### Referencing Test Data from SpecFlow+
You can reference the [[properties|http://specflow.org/api/report/docs/]] by SpecFlow+ to perform calculations and output information on the test run you are interested in. Use the '@' character as a prefix to reference these properties, e.g. `@Model.Configuration.ProjectName` returns the name of your project. 

You can see this in action for yourself. Search for “&lt;body>” in your template to locate the start of the HTML report’s body:

```xml
<body>
        <h1>@Model.Configuration.ProjectName Test Execution Report</h1>
```
The second line defines the top level heading (`h1` element) at the start of the report. [[@Model.Configuration.ProjectName|http://specflow.org/api/report/docs/class_tech_talk_1_1_spec_run_1_1_framework_1_1_configuration_1_1_test_profile_settings.html#a6c54a15903a60ea12189a42731ee2961]] accesses the name of your project while “Test Execution Report” is plain (static) text. As mentioned before, the ‘@’ character is used to denote code sections or variables to embed in your HTML.

Let's make a minor change to the report's heading:

1. Change `@Model.Configuration.ProjectName` to `[[@Model.Configuration.TestProfileSettings.ReportTemplate|http://specflow.org/api/report/docs/class_tech_talk_1_1_spec_run_1_1_framework_1_1_configuration_1_1_test_profile_settings.html#a25b29cff361f816a64c67800199c560e]]`
1. Change “Test Execution Report” to “is my new Test Execution Report template”.  
  The content should look like this:  
	&lt;body>  
        &lt;h1>@Model.Configuration.TestProfileSettings.ReportTemplate is my new Test Execution Report template&lt;/h1>  
2. Run your tests and click on the link to the report to view the output. The header should now be similar to the following:

<img src="http://www.specflow.org/media/EditedHeader.png">

While this is a trivial example, it demonstrates how to integrate information passed by SpecFlow+ in your report and how to include it in the HTML output. The examples below include some more interesting customisations that you can use as the basis for your own templates.

#Examples
The following examples are intended to get you started and give you some ideas for how to customise your own reports:

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
We are going to add a sortable table to display information on the individual steps in a feature file. You can either replace the final table in the default template (`<table class="testEvents">`), or simply add this table to the end of the report (within the `<body>` section). We will include the time taken by each step in the table so we can sort the table by step duration. This makes it easy to identify any steps that are taking a long time to execute and possibly optimise them.

Defining a sortable table using sortable.js is easy: just start your HTML table declaration with the following element:  
`<table class="sortable">`

The remaining definition of the table is standard HTML using `<tr>` and `<td>` elements. We will also need to define an “Index” column to ensure that we can revert the table to the default sort order at any time. The following code initialises the index to 0 (you can obviously start counting from 1 if you prefer) and defines the column headers for each of the columns for our test results:

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
        <pre class="log">@Raw(FormatTechMessages(traceEvent.TechMessages.TrimEnd()))</pre>
        @if (!string.IsNullOrEmpty(traceEvent.Error))
        {
          <div class="errorMessage">@Raw(FormatTechMessages(traceEvent.Error))</div>
           <pre class="stackTrace">@Raw(FormatTechMessages(traceEvent.StackTrace.TrimEnd()))</pre>
         }
    </td>
    <td>@traceEvent.ResultType</td>
    <td>@GetSeconds(Math.Round(traceEvent.Duration.TotalSeconds, 3))s</td>
</tr>
```

Finally, we need to increment the Index by one before looping through the next entry:
```
    Index = Index +1;
}
</table>
```

### Making Things Pretty
You can customise the colours used by the table in the CSS section of the template. Search for `<style type="text/css">` to locate this section. I have used the following settings, setting the header to light grey (#e8eef4) with a black font (#000000), and using alternating blues (#66aaee and #99ccf1) for the table rows:

```
        /* Sortable tables */
table.sortable thead {
    background-color:#e8eef4;   /*header bg color*/
    color:#000000;              /*Header font color*/
    font-weight: bold;
    font-size:large;
    cursor: default;
}

table.sortable tbody tr:nth-child(2n) td {
  background: #66aaee;
}
table.sortable tbody tr:nth-child(2n+1) td {
  background: #99ccf1;
}
/* SORTABLE END*/
```

### Final Steps
While you can now run your tests and generate the report, you still need to ensure that the HTML output can access `sorttable.js`. For now, the just copy the file to your report’s output directory. In a real-life scenario you will probably want to ensure that this file is automatically deployed to this directory whenever you run your tests.

### The Final Output
Once you have copied the JavaScript file to your output directory and run your tests, open the resulting HTML file.

Click on a column header to sort the entries in that column:
<a href="http://www.specflow.org/media/AscendingOrder.png">
<img src="http://www.specflow.org/media/AscendingOrder.png">
</a>

Click in the header again to change between ascending/descending order:
<a href="http://www.specflow.org/media/DescendingOrder.png">
<img src="http://www.specflow.org/media/DescendingOrder.png">
</a>

Click on the Index column's header to return to the default sort order:
<a href="http://www.specflow.org/media/DefaultOrder.png">
<img src="http://www.specflow.org/media/DefaultOrder.png">
</a>
## Including Charts
By default, the SpecFlow+ results output information on the number of tests that were successful, failed, are pending etc. In this example, we are going to display this information as a pie chart as well:

<img src="http://www.specflow.org/media/PieChart.png">

To do so, we are going to use [[Highcharts|http://www.highcharts.com]] to display a [[pie chart|https://jsfiddle.net/gh/get/jquery/1.9.1/highslide-software/highcharts.com/tree/master/samples/highcharts/demo/pie-basic/]]. Other types of charts are also supported by Highcharts, and integrating them is very similar.

### Implementing a Render Function

We will implement a function to render the pie chart that is very similar to the pie chart [[sample code|https://jsfiddle.net/gh/get/jquery/1.9.1/highslide-software/highcharts.com/tree/master/samples/highcharts/demo/pie-basic/]], but we are going to populate the chart with the results data from SpecFlow+. Add the following function to your template – preferably with the other functions. I have added the function after the `doSetHeights` function and before `$(document).ready`:

```
function renderPieChart() {
  $('#chart').highcharts({
    chart: {
      plotBackgroundColor: null,
      plotBorderWidth: null,
      plotShadow: false,
      type: 'pie'
    },
    title: {
      text: ''
    },
    tooltip: {
      pointFormat: '{series.name}: <b>{point.percentage:.1f}%</b>'
    },
    plotOptions: {
      pie: {
        allowPointSelect: true,
        cursor: 'pointer',
        dataLabels: {
          enabled: true,
          format: '<b>{point.name}</b>: {point.percentage:.1f} %',
          style: {
            color: (Highcharts.theme && Highcharts.theme.contrastTextColor) || 'black'
          }
        }
      }
    },
    series: [{
      name: 'Brands',
      colorByPoint: true,
      data: [{
        name: 'Succeeded',
        y: @Model.Summary.Succeeded @*Number of successful tests*@
      }, {
        name: 'Failures',
        y: @Model.Summary.TotalFailure,   @*Number of failed tests*@
          }, {
        name: 'Pending',
        y: @Model.Summary.TotalPending  @*Number of pending tests*@
      }, {
        name: 'Ignored',
        y: @Model.Summary.Ignored   @*Number of ignored tests*@
  }, {
name: 'Skipped',
  y: @Model.Summary.Skipped   @*Number of skipped tests*@
  }]
  }]
  });
}
```

The main things to note in this code:
* “#chart” refers to the ID of the `<div>` element that will contain the chart.
* The names of the individual slices are hard-coded as “Succeeded”, “Failures” etc.
* The data (`series`) used by the chart is specified using `@Model.Summary.XYZ`, where `XYZ` is the value for each slice of the pie chart. You can obviously pass other numeric data from SpecFlow+ (e.g. execution times).

### Rendering the Chart
We still need to render the chart by calling the renderPieChart function once the document is ready. Locate `$(document).ready(function ()`, and add the following line at the end of the function:

`renderPieChart();`

### Including the Chart in the Report
The final step is to include the chart in your report at the appropriate position. In this case, we want to display the pie chart immediately after the overall summary of the test results. Search for `<h2>Result: @Model.Summary.ConcludedResultMessage</h2>` and add the following code after the `</table>` tag:

```
    <script src="https://code.highcharts.com/highcharts.js"></script>
    <script src="https://code.highcharts.com/modules/exporting.js"></script>
    <div id="chart" style="min-width: 310px; height: 400px; max-width: 600px; margin: 0 auto"></div>
```

Note that the ID of the `div` element is “chart”, which matches the value defined in `renderPieChart`. You can move the script references to elsewhere in the document, but make sure they are included!

**Note:** Because the referenced JavaScript files are available online, you do not need to copy the files to your output directory.

##Including Screenshots
A common requirement is to include screenshots in the report. SpecFlow+ Runner does not currently include functions for taking an embedding screenshots. However, you can still include screenshots in your report. The process is a little complicated, and involves passing information on the screenshot to the report using `Console.Write()`. The easiest way to understand how the process works is to look at an existing example. You can download a sample project [[here|https://github.com/techtalk/SpecFlow.Plus.Examples/tree/master/SeleniumWebTest]]. In this project, a screenshot is taken after each step. While this project uses Selenium as the testing framework, the principle is the same for other frameworks as well:

1. Take a screenshot at the right moment during your test run.
1. Save the screenshot to file.
1. Pass the screenshot's file path to the report using Console.Write()
1. Parse the information received by the report to strip out the information relating to the screenshot, and embed the screenshot in the HTML.

**Note:** In order to run Selenium tests with FireFox, you may need to [[download the gecko driver|https://github.com/mozilla/geckodriver/releases]]. Copy `geckodriver.exe` to your `SpecFlow.Plus.Examples\SeleniumWebTest\TestApplication.UiTests\bin\Debug` directory or add it to your system’s PATH environment settings.

Once you have downloaded the solution and installed the gecko driver:

1. Open the solution (`TestApplication.sln`) in Visual Studio.
1. Visual Studio will download the NuGet packages required by the solution.
1. Once the solution has finished loading and installing the packages, build the solution.
1. Switch to the Test Explorer in Visual Studio. You should have 7 tests:  
  [[http://www.specflow.org/media/Screenshots_in_reports_test_explorer.png]]
1. Run the tests to verify that everything is set up correctly. 
1. Once the tests have completed, open the report file (the link is in the **Output** pane in Visual Studio).

###The Report
Scroll down in the report until you reach a **Steps** section. For each successfully completed step, you should see a screenshot in the **Trace** column:  
[[http://www.specflow.org/media/Screenshots_in_reports_output.png]]

###How it Works
Taking screenshots is handled in `Screenshots.cs` in the `TestApplication.UiTests` project’s Support folder:

```
    [Binding]
    class Screenshots
    {
        private readonly WebDriver _webDriver;

        public Screenshots(WebDriver webDriver)
        {
            _webDriver = webDriver;
        }

        [AfterStep()]
        public void MakeScreenshotAfterStep()
        {
            var takesScreenshot = _webDriver.Current as ITakesScreenshot;
            if (takesScreenshot != null)
            {
                var screenshot = takesScreenshot.GetScreenshot();
                var tempFileName = Path.Combine(Directory.GetCurrentDirectory(), Path.GetFileNameWithoutExtension(Path.GetTempFileName())) + ".jpg";
                screenshot.SaveAsFile(tempFileName, ImageFormat.Jpeg);

                Console.WriteLine($"SCREENSHOT[ file:///{tempFileName} ]SCREENSHOT");
            }
        }
    }    
```

The function `MakeScreenshotAfterStep()` is responsible for taking a screenshot once each step is completed. The `[AfterStep()]` [[hook|http://www.specflow.org/documentation/Hooks/]] before the function declaration ensures that this function is executed once each scenario step has been completed.

In this case, the screenshot is taken using the Selenium API: 
```
var screenshot = takesScreenshot.GetScreenshot(); 
```
**Note:** If you are using a different testing framework, replace this with the appropriate screenshot function for your framework.

Once the screenshot has been taken, we need to save the screenshot to the current directory. The file name is stored in `tempFileName`, and used to both save the image file (as a JPG) and to pass the path to the screenshot to the report.

Passing the file path to the report is handled using the console. Any data written to the console is available to the report template. In this case, we are writing the file name with some extra padding (`SCREENSHOT[ <PATH>] SCREENSHOT`) to allow us to uniquely identify file paths in the report template.

The path passed to the report template needs to be processed by the report template so that we can embed the specified image. Open `ReportTemplate.cshtml` (in the `Report` folder of the `TestApplication.UiTests` project). Scroll down to the bottom of the file. The following code is responsible for the content of the **Trace** column in the table:
```
<td>   
   <!-- [@traceEvent.Type: @relatedNode.Type - @relatedNode.Title] -->
   <pre class="log">@Raw(FormatTechMessages(traceEvent.TechMessages.TrimEnd()).Replace("SCREENSHOT[ <a href=", "<img width='1000' src=").Replace("</a> ]SCREENSHOT", "</img>"))</pre>
   @if (!string.IsNullOrEmpty(traceEvent.Error))
   {
      <div class="errorMessage">@Raw(FormatTechMessages(traceEvent.Error))</div>
      <pre class="stackTrace">@Raw(FormatTechMessages(traceEvent.StackTrace.TrimEnd()))</pre>
   }
</td>
```

By default, the file path is passed to the report as a hyperlink (`<a href>`). We want to embed the image in the document (using an `<img>` tag), and remove the padding used to identify the screenshot path (`SCREENSHOT [<PATH>] SCREENSHOT`).

This is handled by the following line:
```
class="log">@Raw(FormatTechMessages(traceEvent.TechMessages.TrimEnd()).Replace("SCREENSHOT[ <a href=", "<img width='1000' src=").Replace("</a> ]SCREENSHOT", "</img>"))</pre>
```

The `SCREENSHOT [` opening padding and the opening hyperlink tag are replaced by the HTML image tag including formatting. The file name is left unchanged. The closing hyperlink tag and `] SCREENSHOT` padding is replaced by a closing image tag. The result is to embed the image in the generated report using the file path passed to the report via the console.


###Other Environments
While this example uses Selenium, it should be easy to edit the function that takes a screenshot after each step to use the appropriate screenshot function for you target environment. What is important to remember is that you can abuse the console to pass extra information to your reports. However, be aware that by default, the console output is simply written to your report “as is”. You will need to parse the data passed by the console in your report template, and remove any information (such as padding) that should not appear in the report. This trick can be used to pass any kind of information, not just paths to screenshots.
