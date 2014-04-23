In order to use SpecFlow+ Excel to extend your scenario outlines with additional examples, you need to decorate the scenario outline examples blocks with a special `@source` tag.

```
@source:excel-file-path[:sheet-name]
```

The `excel-file-path` is a path to the Excel file, relative to the feature file itself. 

You can optionally specify the `sheet-name`. If worksheet name is not specified, the plugin tries to use a sheet named like the scenario outline or uses the first worksheet if there is no match.

The `Examples` block has to contain a header row. The header row in the feature file and the Excel file has to match (same columns, same order).

You can also define concrete examples in the feature file too. In this case, the examples from the Excel file will be merged to the examples defined in the feature file.

See also an example with the [feature file](http://www.specflow.org/media/sfp_exel/Sample-ExcelExamples.feature) and the related [Excel file](http://www.specflow.org/media/sfp_exel/Sample-ExcelExamples.xlsx) with the additional examples.

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

