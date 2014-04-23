The features of SpecFlow+ Excel can also be invoked from a command line tool. The command line tool is located in the `tools` folder of the [NuGet package](http://www.nuget.org/packages/SpecFlow.Plus.Excel).

To get an overview of the possible options, you can invoke the tool without parameters. 

```
SpecFlow.Plus.Excel.Converter.exe
```

To get help about a specific command, use the `help` command:

```
SpecFlow.Plus.Excel.Converter.exe help convert
```

The command line tool also works on non-Windows machines using Mono. In this case you need to invoke the tool through Mono:

```
mono SpecFlow.Plus.Excel.Converter.exe
```

## Available commands

* `convert` Converts an Excel feature file (.feature.xlsx) to plain-text Gherkin file
* `initialize` Initializes an Excel feature file (.feature.xlsx) based on a plain-text Gherkin file (one-time conversion)
* `about` Displays information about the tool and the registration status
* `register` Registers a seat license on the current user
* `unregister` Unregisters the product for the current user

## Convert

The `convert` command can be used to transform an Excel feature file to plain-text Gherkin file format.

Usage:
```
SpecFlow.Plus.Excel.Converter.exe convert excelFilePath outputFeatureFilePath [/lang:value] [/culture:value]
```

* `excelFilePath` The Excel file path
* `outputFeatureFilePath` The output feature file path
* `[/lang:value]` The default Gherkin language to be used to convert the Excel file, default: en-US
* `[/culture:value]` The culture to be used to format cell values (e.g. dates), default: same as `lang`. See [[Converting Excel Cells]] for details.

## Initialize

The `initialize` command can be used to create an Excel feature file from an existing plain-text feature file. This can also be used to experiment how the different Gherkin elements are represented in Excel.

Usage:
```
SpecFlow.Plus.Excel.Converter.exe initialize featureFilePath outputExcelFilePath [/lang:value]
```

* `featureFilePath` The feature file path
* `outputExcelFilePath` The outputh Excel file path
* `[/lang:value]` The default Gherkin language to be used to convert the feature file, default: en-US

## Register

The `register` command can be used to register your license key. The registration is valid for all SpecFlow+ components. You can use the `about` command to display your current registration status.

Usage:
```
SpecFlow.Plus.Excel.Converter.exe register licenseKey issuedTo
```

* `licenseKey` The license key
* `issuedTo` The exact 'issued to' value that was specified for the purchase. Please use quotes if the 'issued to' value of your license contains whitespaces. **The 'issued to' value is usually the email address you have used for purchasing SpecFlow+.**

Example:
```
SpecFlow.Plus.Excel.Converter.exe register KGg45...A== "John Doe"
```
