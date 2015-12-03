The SpecFlow+ Excel plugin allows you to extend scenario outline in plain text with Excel tables. Add the Excel files containing these test examples to your project so that the examples can be used by your executable tests. See [SpecFlow+ Excel Getting Started](http://www.specflow.org/plus/excel/getting-started/) for a quick introduction.

The sample [feature file](http://www.specflow.org/media/sfp_excel/Sample-ExcelExamples.feature) and the related [Excel file](http://www.specflow.org/media/sfp_excel/Sample-ExcelExamples.xlsx) include additional examples.

## Using the Same Excel File to Describe Multiple Example Sets

One Excel examples file can be used to describe multiple example sets of even multiple scenario outlines. In this case, each worksheet should contain a single example set. In general, you should create an Excel examples file for each feature file. You can specify the name of the Excel sheet explicitly in the feature file, but this is not necessary if you name your sheets the same as your scenario outline titles. For more details, see [[Prepare Feature Files for External Examples]].

## Converting Excel Cell Values

Cell values, in particular non-string values like dates or numbers, are converted using a specific culture when executing tests. Cell formatting options in Excel (e.g. number of decimal places, rounding, currency signs, date formats) are ignored. See [[Converting Excel Cells]] for more details.
