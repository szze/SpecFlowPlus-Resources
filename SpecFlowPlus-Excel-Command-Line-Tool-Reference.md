You can invoke SpecFlow+ Excel's features using the command line tool located in the `tools` folder of the [NuGet package](http://www.nuget.org/packages/SpecFlow.Plus.Excel).

If you start the tool without any parameters, the available options are summarised: 

```
SpecFlow.Plus.Excel.Converter.exe
```

For help about a specific command, use the `help` command:

```
SpecFlow.Plus.Excel.Converter.exe help convert
```

The command line tool also works on non-Windows machines using Mono. In this case you need to invoke the tool through Mono:

```
mono SpecFlow.Plus.Excel.Converter.exe
```

## Available commands

* `convert`: Converts an Excel feature file (.feature.xlsx) to a plain text Gherkin file
* `initialize`: Initializes an Excel feature file (.feature.xlsx) based on a plain-text Gherkin file (one-time conversion)
* `about`: Displays information about the tool and your license
* `register`: Registers a license
* `unregister`: Unregisters the license

## Convert

Use the `convert` command to transform an Excel feature file to plain text Gherkin file.

Usage:
```
SpecFlow.Plus.Excel.Converter.exe convert excelFilePath outputFeatureFilePath [/lang:value] [/culture:value]
```

* `excelFilePath`: The Excel file's path
* `outputFeatureFilePath`: The generated Gherkin feature file's target path
* `[/lang:value]`: The Gherkin language used to convert the Excel file; **default:** en-US
* `[/culture:value]`: The culture used to format cell values (e.g. dates); **default: same** as `lang`. For more details on how values are converted, see [[Converting Excel Cells]].

## Initialize

Use the `initialize` command to create an Excel feature file from an existing plain text feature file. You can also use this option to experiment with how different Gherkin elements are represented in Excel.

Usage:
```
SpecFlow.Plus.Excel.Converter.exe initialize featureFilePath outputExcelFilePath [/lang:value]
```

* `featureFilePath`: The feature file's path
* `outputExcelFilePath`: The generated Excel file's target path
* `[/lang:value]`: The default Gherkin language used to convert the feature file; **default:** en-US

## Register

Use the `register` command to register your license key. You only need to register your license once for all SpecFlow+ components. Use the `about` command to display your current license status.

Usage:
```
SpecFlow.Plus.Excel.Converter.exe register licenseKey issuedTo
```

* `licenseKey`: The license key
* `issuedTo`: The exact 'issued to' value of the license. If you ordered SpecFlow+ via SWREG, this is the mail address used to purchase SpecFlow+. If you purchased SpecFlow+ directly from TechTalk, this value is specified in the email you received with your license details.
**Note:** If your 'issued to' value contains spaces, enclose it with quotation marks

Example:
```
SpecFlow.Plus.Excel.Converter.exe register KGg45...A== "John Doe"
```
