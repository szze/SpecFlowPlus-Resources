YAML is whitespace sensitive. Please copy and paste the example in a text editor with syntax highlighting (e.g. Notepad++)

[[Reference guide to Azure Pipelines YAML schema | https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema?view=azure-devops&tabs=schema#task]]

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

* **task:** techtalk.techtalk-specflow-plus.specflow-plus.SpecFlowPlus@0
    - _@value is the task version number_

### LivingDoc specific parameters (inputs):

* **displayName:** (required)
* **projectFilePath:** The project file (*.csproj) containing the feature files (required)
* **projectName:** The name of the project visible in the viewer
* **projectLanguage:** [[Gherkin languages | https://docs.cucumber.io/gherkin/reference/#overview]]
* **workItemPrefix:** The special tag you mark the scenarios with to link them to the respecting work items

### Non-LivingDoc specific parameters:

* **enabled:** boolean (not needed when true)
* **continueOnError:** boolean  (not needed when false)
* **condition:**

| selection | YAML value |
| --- | --- |
| Only when all previous tasks have succeeded | (nothing) |
| Even if a previous task has failed, unless the build was canceled | succeededOrFailed() |
| Even if a previous task has failed, even if the build was canceled | always() |
| Only when a previous task has failed | failed() |
| Custom conditions | (custom condition)

* **timeoutInMinutes:** Specifies the maximum time, in minutes, that a task is allowed to execute before being canceled by server (zero value indicates an infinite timeout)