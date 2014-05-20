SpecFlow+ Runner provides advanced integration with Visual Studio Test Explorer. After building the solution, the business readable scenario titles will show up in Visual Studio Test Explorer.

Among others, you can configure the [[SpecFlow+ Runner test profile|SpecFlowPlus Runner Test Profiles]] to be used, the generated report file name and also the custom traits to be applied to SpecFlow+ Runner tests for better searchability.

## Execution defaults

When running the tests from the Test Explorer window, the tests are executed according the following defaults.

### Profile

SpecFlow+ Runner uses [[test profiles|SpecFlowPlus Runner Test Profiles]] to configure the test suite and the execution details. The Test Explorer integration looks for the `VisualStudio.srprofile` in your project. If that does not exists it uses the `Default.srprofile`.

### Processor Architecture

Unless specified in the test profile otherwise the execution uses test processor architecture setting of Visual Studio. This is set to `x86` by default in Visual Studio 2013. 

You can change this setting from Visual Studio with _Test_ / _Test Settings_ / _Default Processor Architecture_ menu options.

### Report file

SpecFlow+ Runner generates a report file based on the project name and the current timestamp by default.

## Custom configuration

In order to specify a custom configuration, you need to use a combination of [Visual Studio test settings file](http://msdn.microsoft.com/en-us/library/jj635153.aspx) and the SpecFlow+ Runner test profile. To accomplish you need to perform the following steps:

1. Create a test settings file based on the file template located at `packages/SpecRun.Runner.{version}/docs/Sample.runsettings` using the _Add Existing Item..._ dialog.
2. Change settings in the created run settings file if needed (see below).
3. Activate the run settings file with the _Test_ / _Test Settings_ / _Select Test Settings File_ menu option.

### General run settings

SpecFlow+ Runner uses the following Visual Studio general settings. You can find details about these settings on [MSDN](http://msdn.microsoft.com/en-us/library/jj635153.aspx).

* `ResultsDirectory` - The directory where test results will be placed.
* `TargetFrameworkVersion` - Default target framework version (for testing with the .NET 3.5 framework, set the `TargetFrameworkVersion` to `Framework40` and use the SpecFlow+ Runner profile to specify .NET 3.5)
* `TargetPlatform` - Default processor architecture (can be overridden from SpecFlow+ Runner profile)

Sample run settings file with general settings:

```xml
<RunSettings>
  <RunConfiguration>
    <ResultsDirectory>.\TestResults</ResultsDirectory>
    <TargetPlatform>x86</TargetPlatform>
    <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>
  </RunConfiguration>
  ...
</RunSettings>
```

### SpecFlow+ Runner settings

The SpecFlow+ Runner settings can be specified in the run settings file in a `<SpecRun>` element. See section "Execution defaults" for the default settings.

Available options:

* `Profile` - Specifies the SpecFlow+ Runner [[test profile|SpecFlowPlus Runner Test Profiles]] to be used. 
* `ReportFile` - Specifies the report file name to be generated. 
* `GenerateSpecRunTrait` - if set to `true`, it marks all SpecFlow+ Runner tests with a `SpecRun` trait. This might be useful for distinguishing SpecFlow+ Runner tests from unit tests in the Test Explorer window.
* `GenerateFeatureTrait` - if set to `true`, it marks all SpecFlow+ Runner tests with traits using the feature title. The "Group by Class" view of the Test Explorer window can also be used to group tests by feature.

Sample run settings file with SpecFlow+ Runner settings:

```xml
<RunSettings>
  <RunConfiguration>
    ...
  </RunConfiguration>

  <!-- Configurations for SpecFlow+ Runner -->
  <SpecRun>
    <Profile>MyProfile.srprofile</Profile>
    <ReportFile>CustomReport.html</ReportFile>
    <GenerateSpecRunTrait>false</GenerateSpecRunTrait>
    <GenerateFeatureTrait>false</GenerateFeatureTrait>
  </SpecRun>
</RunSettings>
```

