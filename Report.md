|Attribute     |Required/Optional|Description|
|--------------|-----------------|-----------|
|disable       |Optional         |Set this attribute to true to disable the report generation (default: `false`)|
|copyAlsoToBaseFolder|Optional   |Set this to true to also copy all the generated reports to the base folder (default: `false`)|
|Template      |Optional         |Use this element to define the template(s) used to generate reports. You can specify any number of templates; a report will be generated using each template specified. More details on the available attributes can be found below.|

## Template Element
Use the `<Template>` element to specify the templates used to generate reports and the behaviour of the output file. You can generate multiple reports by defining multiple `<Template>` elements, one for each report.

The following attributes are available:

|Attribute     |Description|
|--------------|-----------------|
|name          |The path to the template .cshtml file, relative to the base folder|
|outputName    |The path of the generated report, relative to the base folder.<br><br>You can use the following placeholders in file names to ensure the name is unique:<br>`{now}`: A timestamp with the current date and time<br>`{unique_guid}`: Unique GUID|
|existingFileHandlingStrategy| Determines the behaviour if an existing file with the same name already exists. Possible values:<br>`Overwrite` (default): Overwrites existing files with the same name.<br>`IncrementFilename`: Follows the Windows paradigm of adding an incremental suffix (e.g. "(1)", "(2)" etc.) to the end of file names. This will retain the existing file with its original name and result in a new file being generated with the appropriate incremental suffix. |

**Note:** The report template specified in the [[&lt;Settings>|Settings]] element (`reportTemplate`) is used in addition to the templates specified in the `<Report>` element.

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

