The SpecFlow+ Excel uses the following rules to convert the cell values.

* Always the cell values and not the formulas
* Formatting (e.g. currency or date format) is ignored
* The binding culture is used to convert the cell values back to string for test input.
* The binding culture is the default Gherkin language of the project, but can overridden. See [SpecFlow documentation](http://www.specflow.org/documentation/Feature-Language/) for details.