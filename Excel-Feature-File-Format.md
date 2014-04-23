## General rules

_Note:_ The rule descriptions use English Gherkin keywords, but the SpecFlow+ Excel plugin supports all 50+ languages supported by Gherkin itself. You can also use the different keyword variations as well (like `Scenario Outline` and `Scenario Template`).

* The Excel feature file has to use `.feature.xlsx` extension, e.g. `Calculator.feature.xlsx`. The [[build-time generation|Working with Generated files (SpecFlowPlus Excel)]] of SpecFlow will only convert Excel files in the project with this extension.
* Consider the [[general cell conversion rules|Converting Excel Cells]], especially for non-string cell values.
* You can use the Excel worksheets and cells for helper calculations and comments that should not be part of the feature file. SpecFlow+ Excel will ignore
  * the hidden sheets or the sheets with name prefixed with underscore (`_`)
  * the cell values that you put on the right side (separated by at least two empty cells)
*  The step text can be split into multiple cells. The cells are merged with a single space during processing.
* You can use Excel formulas anywhere in the document. The plugin processes the formula result.
* Cell ranges can be used to specify Gherkin tables. These cell ranges has to be "indented" by one column, ie. the first cell has to be left empty.

## Excel features matching to the Gherkin feature file structure

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
<td>`Title` document property, or the file name if empty.</td>
</tr>
<tr>
<td>Feature tags</td>
<td>`Keywords` document property, separated by whitespace or comma. The `@` prefix is not required.</td>
</tr>
<tr>
<td>Feature language</td>
<td>Put `language:lang-code` into the `Category` document property. For SpecFlow, the project defaults are used.</td>
</tr>
<tr>
<td>Scenario or Scenario Outline</td>
<td>Worksheets (except ignored or background)</td>
</tr>
<tr>
<td>Scenario title</td>
<td>The name of the sheet or a line in the top of the sheet with the first cell as `Scenario:` or `Scenario Outline:` and followed by a cell with the title text. The Excel sheet names can contain maximum 31 characters, so for longer scenario titles, you have to use the second option.</td>
</tr>
<tr>
<td>Scenario tags</td>
<td>One ore more lines in the tip of the sheet with cells containing tags, including the leading `@`. The tags can be split to multiple cells or separated with whitespace.</td>
</tr>
<tr>
<td>Background</td>
<td>A sheet named `Background`.</td>
</tr>
<tr>
<td>Scenario Outline</td>
<td>A sheet, like for a Scenario, but with an Examples section.</td>
</tr>
<tr>
<td>Scenario Outline Examples</td>
<td>Start a line with a cell containing `Examples:`. You can use the next cell to specify a title for the examples block (optional). You can also add lines with tags directly before this line. The examples table can be specified as Excel cells, but they need to be "indented" by one column, ie. the first cell has to be left empty.
![Scenario Outline Examples](http://www.specflow.org/media/sfp_excel/excel-feature-examples.png)
</td>
</tr>
<tr>
<td></td>
<td></td>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</tbody>
</table>