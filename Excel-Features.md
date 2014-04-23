The SpecFlow+ Excel plugin allows you to describe your features in Excel files instead of the normal, plain-text Gherkin feature files. Just like the normal feature files, these Excel feature files can also be added to the project so that all of its scenarios can be used as an executable test.

As the Excel feature file has to represent the structure of the normal pain-text feature files, you have to follow some rules when editing these Excel files. These rules are designed in a way, that they should not restrict you much of the normal Excel working, because the tool uses the matching Excel concepts wherever possible (e.g. you can use the worksheets as scenarios or scenario outlines). See the [[Excel feature file format]] page for the detailed description of the rules. 

See also our [sample Excel feature file](http://www.specflow.org/media/sfp_excel/Sample-ExcelFeature.feature.xlsx).

## Converting plain-text feature files to Excel

The command line tool of SpecFlow+ Excel allows you to generate an initial Excel file from an existing feature file. This can also be used to experiment how the different Gherkin elements are represented in Excel. See [[Command-line tool reference|SpecFlowPlus Excel Command Line Tool Reference]] for details.

## Converting Excel cell values.

The cell values, especially the non-string cell values, like dates or numbers are converted to test using a specific culture. The cell formatting (like display rounding, currency signs, date formats) are not kept. See [[Converting Excel Cells]] for details.

## Multi-language support

In the documentation we use the English Gherkin keywords (like Given, When, Then or Scenario Outline), but the SpecFlow+ Excel plugin supports all 50+ languages supported by Gherkin itself. So you can create your Excel feature file in the language of your own domain!

