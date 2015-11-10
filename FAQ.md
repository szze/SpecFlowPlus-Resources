***Note:*** *Don't forget to check out the [[SpecFlow FAQ|http://www.specflow.org/documentation/FAQ/]] as well.*

### I'm trying to run my SpecFlow+ Runner tests in Visual Studio test window, but they fail with an assembly load error

In some cases the cache folder of Visual Studio Test Adapter gets corrupted. You need to clear the cache to resolve this:

1. Close all Visual Studio instances
2. Open the folder `%TEMP%\VisualStudioTestExplorerExtensions\`
3. Delete all folders named `*SpecRun*`

### I'm trying to use 32-bit assemblies on a 64-bit machine and receive a System.BadImageFormatException despite setting the environment to x86 in my .srprofile
This is a known issue. As a workaround, you need to set SpecRun.exe to run as a 32-bit process. Do this via the [[Visual Studio/Developer Command Prompt|https://msdn.microsoft.com/en-us/library/ms229859%28v=vs.110%29.aspx]] as follows:
corflags YourFolder\SpecRun.exe /32BIT+.