The SpecFlow+ server can be used to store execution statistics for your tests. This data forms the basis for executing tests using the "Adaptive" `testSchedulingMode` in your [[profile|SpecFlowPlus-Runner-Profiles]]. Information on setting up the server can be found [[here|Setting-up-the-SpecFlowPlus-Runner-Server]].

## Adaptive Tests Scheduling
SpecFlow+ uses the test history to determine the order that tests are executed when using the "Adaptive `testSchedulingMode`. Previously failing tests and new tests are executed before successful and stable tests.

Use the "Adaptive" test scheduling mode to prioritise tests failing tests, particularly in combination with the `stopAfterFailures` setting.

## Data in the Database
The execution statistics are stored in an SQL database. The TestItems store data on the previous test results. This is in a format similar to the following:
```
<d:TestHistoryRaw>[{"Result":100,"ExecutionTime":"00:00:05.3810000"},
{"Result":100,"ExecutionTime":"00:00:05.5930000"},{"Result":100,"ExecutionTime":"00:00:04.5470000"},
{"Result":100,"ExecutionTime":"00:00:05.7500000”},{"Result":100,"ExecutionTime":"00:00:08.9010000]</d:TestHistoryRaw>
```

The test results per execution are stored separately (comma-separated). For each test execution, the result of the test and the execution time are stored.

The following result values are used:  
* Unknown = 0
* Succeeded = 100
* Ignored = 200
* Pending = 300
* RandomlyFailed = 390
* Failed = 400

The SQL database also contains a table called Events, that also contains information on the time a test was executed, the machine, the configuration etc.

## Accessing the Database via HTTP

The execution statistics in the database are also partially accessible via HTTP using the following URLs:  
`<Server>:<Port>/read/TestItems`
`<Server>:<Port>/read/Projects`

You can append queries to the URL, such as `[…]/TestItems?$filter=(ProjectId eq guid'745C3D6E-FFC9-4ED9-AE7D-F6FA2102D4AC') and (indexof(Path, ‚cart‘) ge 0)`

By default, the information is displayed as an RSS field, but if you display the source code, you can view the data itself.