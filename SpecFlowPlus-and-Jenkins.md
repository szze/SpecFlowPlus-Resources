*Note: General information on installing Jenkins can be found [[here|https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins]].*

The following steps assume that you are using the [[Git plugin|https://wiki.jenkins-ci.org/display/JENKINS/Git+Plugin]] to handle your source files. You will also need to install the [[MS Build plugin|https://wiki.jenkins-ci.org/display/JENKINS/MSBuild+Plugin]]. You probably also want to install the [[HTML Publisher plugin|https://wiki.jenkins-ci.org/display/JENKINS/HTML+Publisher+Plugin]] to handle reports.

If Visual Studio is not installed on the build server, you will also need to install [[nuget.exe|	https://dist.nuget.org/win-x86-commandline/latest/nuget.exe]] and the [[Agents for Visual Studio|https://www.microsoft.com/en-us/download/details.aspx?id=48152]].

To configure your build process in Jenkins to execute tests using SpecFlow+ Runner:

1. Start the Jenkins web interface.
1. Click on **New Item** to add a new project if you have not already set up a project:  
  1. Enter a name for your project.
  1. Choose "Freestyle project" from the list.
1. On the Jenkins main screen, select **Manage Jenkins** and then **Global Tool Configuration**.
  1. Add a configuration for MSBuild. Give it a meaningful **Name** (e.g. “MSBuild”) and enter the **Path to MSBuild**.
  1. Add a configuration for VSTest as well, including the **Path to VSTest**. 
1. Select **Configure** From the project's main page.
1. Enable **Git** under **Source Code Management**.
1. Enter your **Repository URL**, e.g. “https://github.com/Me/MyProject.git”. You can also enter your login credentials.
1. Specify which branch to build under **Branches to build**, e.g. “\*/master”.
1. Enable **Delete workspace before build starts** under **Build Environment**, otherwise your test results may be incorrect due to the existing TRX files.
1. Click on the **Advanced** button.
1. Click on **Add** next to **Patterns for files to be deleted**:
  Exclude the following:  
  .git/\*\*, TestResults, TestResult/\*.html
1. Click on **Add build step** under **Build** and select **Execute Windows batch command**.
1. Add the following **Command**:  
  “C:\PATH\nuget.exe” restore “C:\PATH\MySpecs.sln”  
  Replace “PATH” with the full path to nuget.exe and your solution. This ensures that your NuGet packages are restored each build.
1. Select the MSBuild configuration you defined in the **MSBuild Version** field under **Build a Visual Studio project or solution using MSBuild**.
1. Enter the path to your solution in the **MSBuild Build File** field.
1. Configure your unit tests to run with VSTest.console:  
  * Select the configuration you defined earlier in the **VStest Version** field.
  * **Test Files**: Enter the path to the assemblies to be tested here.
  * **Specify a logger for test results**: Select trx.
  * **Command Line Arguments**: Enter `/TestAdapterPath:”C:\PATH\packages”` (replace “C:\PATH\” with the path to your solution’s directory).

## SpecFlow+ Execution Reports (optional)
The SpecFlow+ execution reports are stored in the TestResults directory of your project. To be able to easily access these reports from the project overview in Jenkins:

1. Under **Post-build Actions**, click on **Add post-build action** and select “Publish HTML reports”.
1. Enter the path to your project’s TestResults directory under **HTML dir to archive**.
1. Set the **Index Pages** to “ProjectName_ProfileName\*.html” (replace “ProjectName and ProfileName with the name of your project and profile respectively) to reflect the SpecFlow+ report naming convention.

The results of your tests are also visualized by the Jenkins interface, e. g. in the build history and graphs. This information is taken from the TRX file generated by MSTest, which needs to be published as well:

1. Under **Post-build Actions**, click on **Add post-build action** and select “Publish MSTest test result report”. 
1. Enter “\*\*/TestResults/\*.trx” in the **Test report TRX file** field under **Publish MSTest test result report**.
