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

### The Test Explorer is not showing any feature scenario tests

If cleaning your solution and rebuilding does not fix this issue, try deleting the contents (all folders and files) in your `%temp%\VisualStudioTestExplorerExtensions` folder.

### My tests are not displayed in the Test Explorer in Visual Studio 2015.
This is an issue caused by a change in how Visual Studio handles solution-level packages. You can fix this issue by reinstalling the SpecFlow+ Runner NuGet packages or by adding the dependency on the `SpecRun.Runner` package to `packages.config` (`<package id="SpecRun.Runner" version="1.2.0" />`).

### I have updated SpecFlow+ and my test are no longer running

If you have updated SpecFlow+ with a new NuGet package, and are having issues, please check whether the previous versions have been removed completely. Visual Studio does not always remove previous packages when updating. If this happens, the wrong (earlier) version of SpecFlow+ may be used by Visual Studio which can cause version conflicts.

1. Switch to the folder containing your solution in Windows Explorer.
1. Open the `packages` directory.
1. If you see directories with an older version number in the name, delete those directories until you only have 1 directory for each NuGet package.
1. If you are using Visual Studio 2013 or earlier, remove any references to older packages in `packages.config` in your solution. **Note:** This file is not present in Visual Studio 2015.

### I receive a message that I do not have permission to execute install.ps1 when installing SpecFlow+

The installation executes a powershell script. If you do not have permission to execute this script on the machine, the installation will fail. If you do not have the necessary privileges, try entering the following command in the NuGet console:  
`PM> Set-ExecutionPolicy RemoteSigned`  

Once the command has executed, restart the installation process.

<h2 id="upgrades">Upgrading</h2>
### I am having trouble upgrading from SpecFlow+ 1.3 (or earlier) to a newer version with SpecFlow 2 support
Make sure you follow the steps out lined in the guide on [[updating to SpecFlow 2|http://www.specflow.org/updating-to-specflow-2/]].  
In particular:  

* Make sure you restart Visual Studio as described in the link! You need to do this to flush Visual Studio's cache and ensure the correct version of SpecFlow+ is loaded.
* If you use Visual Studio 2013 (or earlier) make sure you have removed any references to older versions of SpecFlow+ from you 'packages.config' file.

### I have multiple solutions with different versions of SpecFlow+ installed and am observing weird behaviour when switching between solutions. Why?
When loading a solution containing SpecFlow+, Visual Studio caches the SpecFlow+ components. If you open a new solution containing a SpecFlow+ project, Visual Studio will retained the cached version of the SpecFlow+ components in memory. If the version used by the two projects is different, this means that there will be a version mismatch.

You can avoid this issue by either upgrading all your solutions to the same version of SpecFlow+, or by restarting Visual Studio to flush the cache before opening the new solution.
