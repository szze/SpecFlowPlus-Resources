**Note:** While English Gherkin keywords are used in this documentation, the SpecFlow+ Excel plugin supports all 50+ languages supported by Gherkin itself. You can also use the various variations as well (e.g. `Scenario Outline` and `Scenario Template`).

We recommend checking out our [sample Excel feature file](http://www.specflow.org/media/sfp_excel/Sample-ExcelFeature.feature.xlsx) first to get an idea of how the files are structured.

## Naming Feature Files
Excel feature file must have the `.feature.xlsx` extension, e.g. `Calculator.feature.xlsx`. SpecFlow's [[build-time generation|Working with Generated files (SpecFlowPlus Excel)]] can only convert Excel files in your project with this extension.

## Cell Content
The content in your Excel files is converted by SpecFlow+ Excel using the following rules:  

* If a cell contains a formula, the result of the formula is used
* Formatting (e.g. currency or date format) is ignored
* The binding culture is used to convert cell values to strings for your tests 
* The binding culture is the default Gherkin language of your project, but can overridden. See [[SpecFlow documentation|http://www.specflow.org/documentation/Feature-Language/]] for more details.

**Note:** Gherkin tables do not support merged cells. If your Excel table contains merged cells, the first of the merged cells will contain the value; the other merged cells will be empty.
<!-- I don't understand a word of the above sentence -->

### Ignored Content
Certain content in your Excel files is ignored by SpecFlow+ Excel. You can use this content for comments, helper calculations etc.

The following is ignored:

  * Data on hidden sheets or sheets whose name begins with an underscore ('_')
  * Cell values where there are at least 2 empty cells to the immediate left of the cell (i.e. use two empty columns to separate comments from data). This includes rows where the first two cells are empty.
  * Empty rows

## Defining Steps
Each step must be defined on a separate row. The step can be split up over multiple cells in the same row, in which case it is treated as though there is a space between the content of neighbouring cells.

## Using Formulas
You can use Excel formulas anywhere in the document. The plugin uses the result of the formula, so you can use formulas to calculate test data values.

## Using Tables
Cell ranges can be used to specify Gherkin tables. These cell ranges must to be "indented" by one column, ie. the first cell has to be left empty.
<!-- I have no idea what this means; can't I just define my data in the table? I've never defined a cell range before and it worked fine -->

## Gherkin Equivalents in Excel
The contents of an Excel file are converted to the Gherkin syntax automatically. The contents of the Excel file are mapped to the Gherkin syntax as follows:

<table>
<thead>
<tr>
<th>Gherkin</th>
<th>Excel</th>
</tr>
</thead>
<tbody>
<tr>
<td>Feature</td>
<td>Workbook (Excel file) with extension `.feature.xlsx`</td>
</tr>
<tr>
<td>Feature title</td>
<td>Defined using the Excel file's `Title` property (<b>File | Info</b>). If no title has been defined, the file name is used instead.</td>
</tr>
<tr>
<td>Feature tags</td>
<td>Defined using the Excel file's `Keywords` property (<b>File | Info</b>, select <b>Advanced Properties</b> from the <b>Properties</b> drop-down list). Separate keywords using whitespace or a comma. The `@` prefix is not required.</td>
</tr>
<tr>
<td>Feature language</td>
<td>Defined using the Excel file's `Categories` property. Enter `language:lang-code` in the field. For SpecFlow, the project defaults are used.
<!--- What does this last sentence mean? ---></td>
</tr>
<tr>
<td>Scenario or Scenario Outline</td>
<td>Worksheets (except ignored or background)</td>
</tr>
<tr>
<td>Scenario title</td>
<td>Taken from either the name of the sheet, or can be defined in the first cell (top left) using `Scenario:` or `Scenario Outline:` followed by the title in the next cell. Excel sheet names can contain a maximum of 31 characters, so for longer scenario titles, you need to use the second option.</td>
</tr>
<tr>
<td>Scenario tags</td>
<td>Defined in one or more lines at the top of the sheet. Include the leading '@' in your tags. Tags can either be entered in a single cell and separated using whitespace, or entered in multiple cells..</td>
</tr>
<tr>
<td>Scenario steps (Given/When/Then)</td>
<td>Each scenario step must be on a separate row. The step's text can be split over multiple cells or entered in a single cell. Splitting the text over multiple cells allows you to use formulas easily, and generally makes it easier to format the scenario's steps.</td>
</tr>
<tr>
<td>DataTable step argument</td>
<td>You can define a table argument (called DataTable in Gherkin) for your steps. To define a DataTable, add the rows after the step and indent each row of the DataTable by one column (i.e. the first cell must be empty).
</td>
</tr>
<tr>
<td>DocString step argument</td>
<td>You can add multi-line text arguments (called DocString in Gherkin) to your steps. To do so, leave the first cell empty in the row after a step, and include the DocString parameter in the second cell (including newlines). The DocString argument cannot be split over multiple cells.</td>
</tr>
<tr>
<td>Background</td>
<td>A sheet named `Background`.</td>
</tr>
<tr>
<td>Scenario Outline</td>
<td>A sheet (like for a Scenario) but with an Examples section.</td>
</tr>
<tr>
<td>Scenario Outline Examples</td>
<td>To define scenario outline examples, start a row with a cell containing `Examples:`. Use the next cell to specify a title for the examples block (optional). If you want to define tags, do so on the previous row.<br>The example data needs to be indented by one column (i.e. the first cell must be empty) and should contain a header with the names of the placeholders. You can define multiple examples block for a scenario outline.
![Scenario Outline Examples](http://www.specflow.org/media/sfp_excel/excel-feature-examples.png)
</td>
</tr>
<tr>
<td>Comments</td>
<td>You can explicitly mark a row as a comment by starting the first non-empty cell with `#`.</td>
</tr>
</tbody>
</table>