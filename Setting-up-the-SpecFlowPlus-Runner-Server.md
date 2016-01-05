The SpecFlow+ Runner server collects execution statistics for your tests at a central location and uses this data to improve the efficiency of your test execution. For example, you can determine which tests are executed first based on the previous execution results, e.g. execute failing tests first.

To install the SpecFlow+ Runner server:

1. Before proceeding, install SpecFlow+ Runner from within Visual Studio, as you will need to copy the contents of the `Server` directory to your server. For details on installing SpecFlow+ Runner, refer to the beginning of the [[Getting Started|http://www.specflow.org/getting-started/]] guide for SpecFlow.
1. Create a new SQL database instance used to store the execution statistics.
1. Copy the contents of the “server” directory to the server.
1. Enter your database connection string in the `<Connection Strings>` element of the SpecRun.Server.exe.config file.
1. Initialise the database using `SpecRun.exe initdatabase` from the command line.
1. Start the service using `SpecRun.exe start` from the command line. **Note:** You may need to assign the service to run under a user with appropriate permissions.
1. The connection to the server takes place via port 6365; ensure that your firewall on the server allows connections via this port.
1. Enter the server’s URL in the `.srprofile` file in your Visual Studio project (`<Server ServerURL =”http://MyServer:6365” publishResults=”true”>`).
1. Rebuild your solution and run your tests. You can verify that you have set up everything correctly by checking if records have been added to the database on the server.

You can use these statistics to execute failing and new tests first. To do so, set the `testSchedulingMode` attribute in the `<Execution>` element of your `.srprofile` file to `Adaptive`. SpecRun then uses the statistics in the pass/fail history to determine which tests to run first. Previously failing tests and new tests are executed before successful and stable tests.

