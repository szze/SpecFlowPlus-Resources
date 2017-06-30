*Note: General information on AppVeyor can be found [[here|https://www.appveyor.com/docs/]].*

To configure your AppVeyor build process to execute your test using SpecFlow+ Runner:

1. Create a new `appveyor.yml` file or open your existing file.
1. Add the following `before_build` section to restore the NuGet packages:  
   ```
   before_build:
     - appveyor DownloadFile https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
     - appveyor DownloadFile https://raw.githubusercontent.com/appveyor/ci/master/scripts/nuget-restore.cmd
     - nuget-restore MyProject.sln
   ```
   Replace `MyProject.sln` with the full path to your project, relative to the location of the appveyor.yml file.
1. Add the following `test_script` section to execute the tests and generate the test output for AppVeyor:  
   ```
   test_script:
     - ps: vstest.console /logger:Appveyor "AssemblyPath\MyAssembly.dll" /TestAdapterPath:"PackagesPath\packages"
   ```
   Replace `AssemblyPath` with the path to your assembly and replace `MyAssembly.dll` with the name of your assembly. Replace `PackagesPath` with the path to the packages folder of your solution.
1. Save `appveyor.yml` and use the file to build your application with AppVeyor.

A sample project is available [[here|https://github.com/techtalk/SpecFlow.Plus.Examples/tree/master/AppVeyor_Support]].