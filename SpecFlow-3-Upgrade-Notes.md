## Updating Customised Reports
If you have customised your [[reports]], you will need to update the first line in your report template to use the template with SpecFlow 3.

Change the following line:  
`@inherits TechTalk.SpecRun.Framework.Reporting.CustomTemplateBase<TestRunResult>`

to  
`@inherits SpecFlow.Plus.Runner.Reporting.CustomTemplateBase<TestRunResult>`

