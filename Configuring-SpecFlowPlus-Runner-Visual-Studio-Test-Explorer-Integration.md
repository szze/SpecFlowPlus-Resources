SpecFlow+ Runner provides advanced integration with Visual Studio Test Explorer. After building the solution, the business readable scenario titles will show up in Visual Studio Test Explorer.

## Execution defaults

When running the tests from the Test Explorer window, the tests are executed according the following defaults.

### Profile

SpecFlow+ Runner uses [[test profiles]] to configure the test suite and the execution details. The Test Explorer integration looks for the `VisualStudio.srprofile` in your project. If that does not exists it uses the `Default.srprofile`.

### Processor Architecture

Unless specified in the test profile otherwise the execution uses test processor architecture setting of Visual Studio. This is set to `x86` by default in Visual Studio 2013. 

You can change this setting from Visual Studio with _Test_ / _Test Settings_ / _Default Processor Architecture_ menu options.