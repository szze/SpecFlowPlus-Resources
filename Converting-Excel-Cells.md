The SpecFlow+ Excel uses the following rules to convert cell values:

* If a cell contains a formula, the result of the formula is used
* Formatting (e.g. currency or date format) is ignored
* The binding culture is used to convert cell values to strings for your tests
* The binding culture is the default Gherkin language of your project, but can overridden. See [SpecFlow documentation](http://www.specflow.org/documentation/Feature-Language/) for details.