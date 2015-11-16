***Note:*** *Don't forget to check out the [[SpecFlow FAQ|http://www.specflow.org/documentation/FAQ/]] as well.*

<h1 id="Licensing">Licensing</h1>
##How is SpecFlow+ licensed?
A single license entitles a single user to execute tests with SpecFlow+ on any number of local or remote machines (including build servers). The license is a perpetual license valid for the current release of SpecFlow+ at the time of purchase, and entitles you to free updates for a period of one year. 

More details on SpecFlow+ licensing can be found [[here|http://www.specflow.org/plus/licensing/]].

##How do I register my license for SpecFlow+?
You need to register your license key once per machine (after adding SpecFlow+ to your first project). More information is available [[here|http://www.specflow.org/plus/evaluation/]] and [[here|http://www.specflow.org/plus/documentation/SpecFlowPlus-Excel-Command-Line-Tool-Reference/]].

<h1 id="Licensing">Troubleshooting</h1>
### I'm trying to run my SpecFlow+ Runner tests in Visual Studio test window, but they fail with an assembly load error

In some cases the cache folder of Visual Studio Test Adapter gets corrupted. You need to clear the cache to resolve this:

1. Close all Visual Studio instances
2. Open the folder `%TEMP%\VisualStudioTestExplorerExtensions\`
3. Delete all folders named `*SpecRun*`

### I'm trying to use 32-bit assemblies on a 64-bit machine and receive a System.BadImageFormatException despite setting the environment to x86 in my .srprofile
This is a known issue. As a workaround, you need to set SpecRun.exe to run as a 32-bit process. Do this via the [[Visual Studio/Developer Command Prompt|https://msdn.microsoft.com/en-us/library/ms229859%28v=vs.110%29.aspx]] as follows:
corflags YourFolder\SpecRun.exe /32BIT+.

### My tests are not displayed in the Test Explorer in Visual Studio 2015.
This is an issue caused by a change in how Visual Studio handles solution-level packages. You can fix this issue by reinstalling the SpecFlow+ Runner NuGet packages or by adding the dependency on the `SpecRun.Runner` package to `packages.config` (`<package id="SpecRun.Runner" version="1.2.0" />`).