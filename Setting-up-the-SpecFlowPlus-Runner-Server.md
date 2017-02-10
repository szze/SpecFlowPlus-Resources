The SpecFlow+ Runner server collects execution statistics for your tests at a central location and uses this data to improve the efficiency of your test execution. For example, you can determine which tests are executed first based on the previous execution results, e.g. execute failing tests first.

#Prerequisites
Before you can set up the server, **you need to install the SpecFlow+ Runner NuGet packages** that contain the server components. Information on installing the NuGet packages can be found [[here|SpecFlow--Runner-Installation]].

#Installing the Server
To install the SpecFlow+ Runner server:

1. Create a new SQL database instance used to store the execution statistics.
1. Locate the "server" directory in your solution's `\packages\SpecRun.Runner.x.y.z\tools` directory (created when you install the NuGet package). Copy the contents of the “server” directory to your server.
1. Enter your database connection string in the `<Connection Strings>` element of the SpecRun.Server.exe.config file.
1. Initialise the database using `SpecRun.Server.exe initdatabase` from the command line.
1. Start the service using `SpecRun.Server.exe start` from the command line. **Note:** You may need to assign the service to run under a user with appropriate permissions.
1. The connection to the server takes place via port 6365; ensure that your firewall on the server allows connections via this port.
1. Enter the server’s URL in the `.srprofile` file in your Visual Studio project (`<Server ServerURL =”http://MyServer:6365” publishResults=”true”>`).
1. Rebuild your solution and run your tests. You can verify that you have set up everything correctly by checking if records have been added to the database on the server.

#Adaptive Test Execution Order
You can use these statistics to execute failing and new tests first. To do so, set the `testSchedulingMode` attribute in the `<Execution>` element of your `.srprofile` file to `Adaptive`. SpecRun then uses the statistics in the pass/fail history to determine which tests to run first. Previously failing tests and new tests are executed before successful and stable tests.
