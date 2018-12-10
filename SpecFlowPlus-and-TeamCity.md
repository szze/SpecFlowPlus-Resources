*Note: General information on configuring build steps in TeamCity can be found [[here|https://confluence.jetbrains.com/display/TCD9/Command+Line]].*

To configure your build process in TeamCity to execute tests using SpecFlow+ Runner:

1. Open your project's build steps.
2. Click on **Add build step**.
3. Choose "Command Line" from the dialogue.
4. Configure the build step as follows:  
  * **Run:** Executable with parameters
  * **Command executable:** Enter the path to SpecRun.exe here
  * **Command parameters:** Enter the command line parameters for SpecRun.exe here. Use the `BuildServerRun` option and include `/buildserver:teamcity`.  
  Information on executing command lines in TeamCity is available [[here|https://confluence.jetbrains.com/display/TCD9/Command+Line]]. More details on the SpecFlow+ Runner's command line options can be found [[here|https://specflow.org/plus/documentation/SpecFlowPlus-Runner-Command-Line/]].
5. Click on **Save**.