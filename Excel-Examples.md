The SpecFlow+ Excel plugin allows you to extend scenario outline examples of normal plain-text feature files with Excel tables. The related Excel examples files can also be added to the project so that all of its examples can be used as an executable test. See [SpecFlow+ Excel Getting Started](http://www.specflow.org/plus/excel/getting-started/) for a quick introduction.

See also an example with the [feature file](http://www.specflow.org/media/sfp_exel/Sample-ExcelExamples.feature) and the related [Excel file](http://www.specflow.org/media/sfp_exel/Sample-ExcelExamples.xlsx) with the additional examples.

## Using the same Excel file for describing multiple example sets

One Excel examples file can be used to describe multiple example sets of even multiple scenario outlines. In this case each worksheet contains an example set. Typically an Excel examples file is created per feature file. In the feature file, you can specify the sheet name explicitly but if you name the sheets as the scenario outline titles, this is not necessary. See [[Prepare Feature Files for External Examples]] for details.

## Converting Excel cell values.

The cell values, especially the non-string cell values, like dates or numbers are converted to test using a specific culture. The cell formatting (like display rounding, currency signs, date formats) are not kept. See [[Converting Excel Cells]] for details.
