YAML is whitespace sensitive. Please copy and paste the example in a text editor with syntax highlighting (e.g. Notepad++)

https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema?view=azure-devops&tabs=schema#task

SpecFlow+LivingDoc custom build step YAML example:

```yaml
 steps:
-task: techtalk.techtalk-specflow-plus-test.specflow-plus.SpecFlowPlus@0
  displayName: 'SpecFlow+ build step SpecFlow.Plus.Runner.Specs'
  inputs:
    projectFilePath: Tests/SpecFlow.Plus.Runner.Specs/Features
    projectName: testName
    projectLanguage: en
    workItemPrefix: testPrefix
  enabled: false
  continueOnError: true
  condition: always()
  timeoutInMinutes: 10
```

* **task:**

| type | value |
| --- | --- |
| SpecFlow+LivingDoc  | techtalk.techtalk-specflow-plus.specflow-plus.SpecFlowPlus@0  |
| SpecFlow+LivingDoc Test  | techtalk.techtalk-specflow-plus-test.specflow-plus.SpecFlowPlus@0  |

_where @value is the task version number_

* **displayName:** (required)
* **projectFilePath:** The project file (*.csproj) containing the feature files (required)
* projectName: The name of the project visible in the viewer
* projectLanguage: https://docs.cucumber.io/gherkin/reference/#spoken-languages
* workItemPrefix: The special tag you mark the scenarios with to link them to the respecting work items
* enabled: boolean (not needed when true)
* continueOnError: boolean  (not needed when false)
* condition:

| type | value |
| --- | --- |
| Only when all previous tasks have succeeded | (nothing) |
| Even if a previous task has failed, unless the build was canceled | succeededOrFailed() |
| Even if a previous task has failed, even if the build was canceled | always() |
| Only when a previous task has failed | failed() |
| Custom conditions | (custom condition)

* timeoutInMinutes: Specifies the maximum time, in minutes, that a task is allowed to execute before being canceled by server. A zero value indicates an infinite timeout.