## General Rules

We recommend that you take a look at this sample [feature file](http://www.specflow.org/media/sfp_excel/Sample-ExcelExamples.feature) and its related [Excel file](http://www.specflow.org/media/sfp_excel/Sample-ExcelExamples.xlsx), which includes additional examples for the feature file, before studying rules in detail.

* Values (in particular non-string values) entered in cells are converted according to the [[general cell conversion rules|Converting Excel Cells]].
* You can use Excel formulas in the Excel file. The plugin uses the result of the formula result to execute your tests.
* Empty Excel rows are ignored.
* Merged cells: Gherkin tables do not support merged cells, so merged cells are converted so that the first cell contains the value and the other cells are empty.
* The first row in the sheet is the examples header row, and must match to the header row [[specified in the feature file|Prepare Feature Files for External Examples]] (same columns, same order).

## Excel examples matching to the Gherkin scenario outline examples

<table>
<thead>
<tr>
<th>Excel</th>
<th>Gherkin</th>
</tr>
</thead>
<tbody>
<tr>
<td>Workbook (Excel file)</td>
<td>Container for multiple example sets</td>
</tr>
<tr>
<td>Worksheet</td>
<td>Scenario Outline examples</td>
</tr>
<tr>
<td>Worksheet first row</td>
<td>Examples header. The header row in the feature file and the Excel file must match (same columns, same order).</td>
</tr>
<tr>
<td>Worksheet further rows</td>
<td>Examples table</td>
</tr>
</tbody>
</table>