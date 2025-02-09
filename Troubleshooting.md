This page covers some of the most common issues that you may encounter when using SpecFlow+.

### I'm trying to run my SpecFlow+ Runner tests in Visual Studio test window, but they fail with an assembly load error ("System.IO.FileNotFoundException: Could not load file or assembly")

In some cases the cache folder of Visual Studio Test Adapter gets corrupted. You need to clear the cache to resolve this:

1. Close all Visual Studio instances
2. Open the folder `%TEMP%\VisualStudioTestExplorerExtensions\`
3. Delete all folders named `*SpecRun*`

### I'm trying to use 32-bit assemblies on a 64-bit machine and receive a System.BadImageFormatException despite setting the environment to x86 in my .srprofile
This is a known issue. As a workaround, you need to set SpecRun.exe to run as a 32-bit process. Do this via the [[Visual Studio/Developer Command Prompt|https://msdn.microsoft.com/en-us/library/ms229859%28v=vs.110%29.aspx]] as follows:
corflags YourFolder\SpecRun.exe /32BIT+.

### The Test Explorer is not showing any feature scenario tests

* If you have added SpecFlow+ Runner to your project or updated the installed package, close and restart Visual Studio. This step is necessary to allow Visual Studio to load the SpecFlow+ Runner test adapter and locate your tests.
* If cleaning your solution and rebuilding does not fix this issue, try deleting the contents (all folders and files) in your `%temp%\VisualStudioTestExplorerExtensions` folder.



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

### I am receiving an Exception Code 0xc00000fd when executing my tests. What is causing this?

0xc00000fd is the code for a stack overflow exception. This exception can occur if you access recursive code from your bindings where the recursion is not terminated (or not terminated before a stack overflow exception occurs). The error is most likely in your recursive code itself.

### Why are my failing tests flagged as failing when they pass on a retry?

This is working as intended. If at least one test fails, the test has not passed successfully. If the initial test fails, there is at least one circumstance where the test fails. Were SpecFlow to flag these tests as passing, it would be ignoring the case where the test fails. There can be many reasons why the first test fails and the second passes - the first step is to determine why this is the case.

If you are absolutely sure that the reason the first test fails and all retries pass is not an issue with your code, but with your architecture, you can run your tests with [[VSTest]] and configure a minimum pass threshold.

Setting the test results to "Unified" with a minimum threshold allows you to treat a test as passing if a certain amount of the tests (initial test+retries) pass. This option should be used with great caution. Unless you are 100% certain that the random pass/fail behaviour is not related to your code, **do not use this option**. The option was added for a specific use case: the intial test would **always** fail due to a timeout on a remote server; this was not an issue for retried tests.

Using this option will generate a TRX file where tests will be marked as passing above the pass threshold. This option is not available for SpecFlow+ reports, as the results are only unified when running tests with VSTest.

Remember that a test that sometimes passes and sometimes fails can point to deeper issues with your tests or code, and should not simply be dismissed.