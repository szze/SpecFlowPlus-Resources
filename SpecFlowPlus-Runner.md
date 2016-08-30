SpecFlow+ Runner is a dedicated test runner for SpecFlow that integrates directly with Visual Studio. You can also execute tests from the [[command line|SpecFlowPlus-Runner-Command-Line]].

SpecFlow+ include the following features:

* Visual Studio integration (syntax coloring, auto completion, navigation, skeleton generation, Gherkin table formatting)
* Visual Studio Test Explorer integration (business readable scenario names, run/debug from feature file)
* Advanced test runner features: [[execution profiles|SpecFlowPlus-Runner-Profiles]], [[target environments|SpecFlowPlus-Runner-Profiles#environment-]], attach artifacts to test execution reports, TFS integration, TeamCity integration, [[complex scenario filter expressions|SpecFlowPlus-Runner-Profiles#filter-]]
* Dedicated support for integration test execution ([[config file transformation and deployment steps|https://github.com/techtalk/SpecFlowPlus-Resources/wiki/SpecFlowPlus-Runner-Profiles#deploymenttransformation-]], test targets: re-run tests for different environments and configurations, detect flickering scenarios)
* Parallel test execution (app domain isolation, process isolation, execution results consolidation)
* Advanced test execution scheduling (run previously failing tests first, retry scenarios, execution history available as OData)
* Customisable HTML reports (Razor templates)

If you are new to SpecFlow+, we recommend you follow the [[Getting Started|http://www.specflow.org/getting-started/]] guide that covers installing SpecFlow+ and setting up your first project.