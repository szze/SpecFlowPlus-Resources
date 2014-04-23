## General rules

We recommend checking out our example with the [feature file](http://www.specflow.org/media/sfp_exel/Sample-ExcelExamples.feature) and the related [Excel file](http://www.specflow.org/media/sfp_exel/Sample-ExcelExamples.xlsx) with the additional examples before studying the detailed rules.

* Consider the [[general cell conversion rules|Converting Excel Cells]], especially for non-string cell values.
* You can use Excel formulas anywhere in the document. The plugin processes the formula result.
* The empty Excel rows are ignored.
* Merged cells: Gherkin tables do not support merged cells, so merged cells are converted without merging, ie. the first cell will contain the value and the other cells will be empty.
* The first row in the sheet is the examples header row. It has to match to the header row [[specified in the feature file|Prepare Feature Files for External Examples]] (same columns, same order).

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
<td>Scenario Outline Examples</td>
</tr>
<tr>
<td>Worksheet first row</td>
<td>Examples header. The header row in the feature file and the Excel file has to match (same columns, same order).</td>
</tr>
<tr>
<td>Worksheet further rows</td>
<td>Examples table</td>
</tr>
</tbody>
</table>