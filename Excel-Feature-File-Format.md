## General rules

* The Excel feature file has to use `.feature.xlsx` extension, e.g. `Calculator.feature.xlsx`. The [[build-time generation|Working with Generated files (SpecFlowPlus Excel)]] of SpecFlow will only convert Excel files in the project with this extension.
* Consider the [[general cell conversion rules|Converting Excel Cells]], especially for non-string cell values.
* You can use the Excel worksheets and cells for helper calculations and comments that should not be part of the feature file. SpecFlow+ Excel will ignore
  * the hidden sheets or the sheets with name prefixed with underscore (`_`)
  * the cell values that you put on the right side (separated by at least two empty cells)

## Excel features matching to the Gherkin feature file strucutre

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
<td>Scenario or Scenario Outline</td>
<td>Worksheets (except ignored or background)</td>
</tr>
<tr>
<td>Scenario or Scenario Outline title</td>
<td>The name of the sheet or a line in the top of the sheet with the first cell as `Scenario:` or `Scenario Outline:` and followed by a cell with the title text. The Excel sheet names can contain maximum 31 characters, so for longer scenario titles, you have to use the second option.</td>
</tr>
<tr>
<td></td>
<td></td>
</tr>
<tr>
<td></td>
<td></td>
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