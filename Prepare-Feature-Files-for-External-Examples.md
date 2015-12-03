In order to use SpecFlow+ Excel to extend your scenario outlines with additional examples, you need to extend the scenario outline examples blocks with a special `@source` tag as follows:
```
@source:excel-file-path[:sheet-name]
```

The `excel-file-path` is the path to the Excel file, relative to the feature file itself. 

The `sheet-name` is optional. If no worksheet name is specified, the plugin uses the Excel sheet with the same name as the scenario outline, or the first worksheet in the file if there is no worksheet with a matching name.

The `Examples` block must contain a header row. The header row needs to match in both the feature file and the Excel file (same columns, same order).

You can also define concrete examples in the feature file. In this case, the examples from the Excel file are merged with the examples defined in the feature file. This sample [feature file](http://www.specflow.org/media/sfp_excel/Sample-ExcelExamples.feature) is extended with additional examples by this [Excel file](http://www.specflow.org/media/sfp_excel/Sample-ExcelExamples.xlsx).

```gherkin
Feature: Calculator

Scenario Outline: Add two numbers
	Given I have entered <a> into the calculator 
	And I have entered <b> into the calculator 
	When I press add
	Then the result should be <result> on the screen 

@source:CalculatorExamples.xlsx
Examples:
	| case | a | b | result |
```