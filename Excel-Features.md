The SpecFlow+ Excel plugin allows you to describe your features in Excel files instead of plain text Gherkin feature files. Just like normal feature files, these Excel feature files can be added to your project, allowing you to execute all its scenarios as executable tests. Refer to [SpecFlow+ Excel Getting Started](http://www.specflow.org/plus/excel/getting-started/) for a quick introduction.

As the Excel feature file has to represent the same structure as a pain text feature file, you have to follow some rules when editing these Excel files. These rules are designed so as not to be too restrictive and conform to the normal way of working in Excel (e.g. you can worksheets to represent scenarios or scenario outlines). For a more detailed breakdown of these rules, see [[Excel feature file format]]. You may also want to take a look at this [sample Excel feature file](http://www.specflow.org/media/sfp_excel/Sample-ExcelFeature.feature.xlsx).

## Converting Plain Text Feature Files to Excel Files

SpecFlow+ Excel's command line tool allows you to generate an initial Excel file from an existing feature file. You can also use this to experiment with how the different Gherkin elements are represented in Excel. For more details, see [[Command-line tool reference|SpecFlowPlus Excel Command Line Tool Reference]].

## Converting Excel Cell Values

Cell values, in particular non-string values like dates or numbers, are converted using a specific culture when extuing tests. Cell formatting options in Excel (e.g. number of decimal places, rounding, currency signs, date formats) are ignored. See [[Converting Excel Cells]] for more details.

## Multi-language Support

This documentation uses the English Gherkin keywords (e.g. `Given`, `When`, `Then` and `Scenario Outline`), but SpecFlow+ Excel supports all 50+ languages supported by Gherkin itself. You can therefore create Excel feature files in the language of your own domain!