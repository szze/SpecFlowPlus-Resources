***Note:*** *Don't forget to check out the [[SpecFlow FAQ|http://www.specflow.org/documentation/FAQ/]] as well.*

<h1 id="Licensing">Licensing</h1>

## How is SpecFlow+ licensed?
SpecFlow+ is licensed per user. A single license entitles a single user to execute tests with SpecFlow+ on any number of local or remote machines (including build servers). 

More details on SpecFlow+ licensing can be found [[here|http://www.specflow.org/plus/licensing/]].

## Are SpecFlow+ licenses perpetual or subscription based?

SpecFlow+ licenses are perpetual licenses that include 1 year of upgrades and support. Your license key will unlock all versions of SpecFlow+ released during this 1 year period, as well as any earlier versions. Once the 1-year period is over, the license key will continue to unlock older versions (i.e. those released prior to the end of the upgrade period), but will not unlock versions released after this 1-year period is over. 

You can extend your license period for another year at 50% of the original license fee. Extensions are always from the end of the previous support period.

## What support is included during the support period?
In addition to having access to the latest releases and pre-releases, we provide support for technical issues during the support period. We will attempt to fix all bugs that are reported, and will prioritise these bugs according to their severity. 

## How can I contact support?
If you have a general issue, suggestion or question concerning SpecFlow+, the best place to turn is the SpecRun Google group. The advantage to the Google group is that it is publicly available, which means that any answers can be searched for in the future. It also gives other users the opportunity to contribute to discussions.

You can also contact support directly at support [at] specflow.org. This is the best place to turn if you have licensing and pricing questions. You can also contact us at this email address if your problem involves sensitive information or proprietary code you do not want to be made public.

Issues with the open source SpecFlow project are managed on the GitHub tracker. However, given the open source nature of the project, it can sometimes take a while for issues to be fixed. If you have an issue with the open source SpecFlow project that is affecting your use of SpecFlow+, please contact us by email. Let us know you are a SpecFlow+ customer and provide a link to the GitHub issue (if it exists) so we can prioritise it. There is also a Google group for the open source project, with support provided by the community. This is a good place to ask general questions you may have about SpecFlow.

Support does not extend to training (this includes answering conceptual questions, e.g. about BDD, Gherkin etc.), consulting or custom development/customisation. We can offer these services separately if you are interested.

## How can I report a bug?
If you have found a bug, please contact us directly at support [at] specflow.org or via the SpecRun Google group. Please include as much information as possible as you can, including:  

* Your SpecFlow version
* Your SpecFlow+ version
* Which SpecFlow+ components you are using
* The test runner and version number you are using, as well as information on how you are executing the tests (e.g. include your command line)
* Your Visual Studio version
* Your .NET framework version
* A link to a project that reproduces the issue, if possible
* The SpecFlow section of your app.config file
* Your .srprofile file

How are bugs prioritised?
We will investigate error reports and try and find a fix according to the severity of the issue:  

* **Critical**: The issue prevents you from working (e.g. cannot run tests at all)
* **High**: The issue seriously impacts your ability to work efficiently; the issue requires a cumbersome workaround or certain key features are not working at all.
* **Medium**: The issue has an impact on efficiency or requires a workaround; this includes bugs that do not seriously impact your ability to complete your daily work.
* **Low**: The impact on efficiency is low or a feasible workaround exists. You can continue working, albeit with a minor impact.
* **Cannot be reproduced**: We cannot reproduce an error. We will inform you if this is the case.

If we can reproduce the error and cannot provide a quick fix, we will handle the issue according to its severity. We will also reply to you to keep you up to date on developments.  

* In the case of **critical** errors, we will try to provide a pre-release version with a fix as soon as possible so that you do not have to wait for the next official release.
* **High** severity errors will either be fixed in the next official release (depending on the release schedule) or in a pre-release version.
* **Medium** severity errors will generally be fixed in the next official release, unless doing so would hold back a scheduled release due to the effort required.
* **Low** severity errors will be fixed as necessary, also taking into account the effort required for the fix (low effort fixes are prioritised).
* If we cannot reproduce an issue, we will inform you of this, asking for more information and/or suggesting other possible causes.
This classification may change if suitable workarounds are discovered or you discover additional impacts on your part.
Note that due to external dependencies (e.g. the Gherkin parser), there may be some cases where we are reliant on a fix that is outside of our control. In these cases we will do our best to expedite matters.

## How do I register my license for SpecFlow+?
You need to register your license key once per machine (after adding SpecFlow+ to your first project). More information is available [[here|http://www.specflow.org/plus/evaluation/]] and [[here|http://www.specflow.org/plus/documentation/SpecFlowPlus-Excel-Command-Line-Tool-Reference/]].

# Sales and Pricing

## Are bulk discounts available?

We can offer discounts on larger orders (5+), with the discount depending on the number of licenses. Please contact us at support [at] specflow.org for a quote. 

## Do you work with resellers?

We work with software resellers. If you are a reseller and are interested in purchasing SpecFlow+ licenses for a customer, you can contact us at support [at] specflow.org.

All purchases are handled by TechTalk’s Swiss subsidiary:
TechTalk Software AG
Untere Paulistrasse 6b 
8834 Schindellegi
Switzerland
Company number: CHE-113.692.442
VAT ID: CHE-113.692.442 MWST 

If you are a reseller, please note that purchases made via the webshop are always registered to the email address used to make the purchase. This means purchases via the webshop are not suitable for resellers. Please contact us directly by email so we can register the license to the correct licensee.

Payment by credit card is preferred, although payment by bank transfer is also possible. The license key will be delivered once payment has been confirmed. This may take some time in the case of international bank transfers. International bank transfers will also be subject to bank charges that will depend on your bank and the country you are based in.

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

<h1 id="upgrades">Upgrading</h1>

### I am having trouble upgrading from SpecFlow+ 1.3 (or earlier) to a newer version with SpecFlow 2 support
Make sure you follow the steps out lined in the guide on [[updating to SpecFlow 2|http://www.specflow.org/updating-to-specflow-2/]].  
In particular:  

* Make sure you restart Visual Studio as described in the link! You need to do this to flush Visual Studio's cache and ensure the correct version of SpecFlow+ is loaded.
* If you use Visual Studio 2013 (or earlier) make sure you have removed any references to older versions of SpecFlow+ from you 'packages.config' file.

### I have multiple solutions with different versions of SpecFlow+ installed and am observing weird behaviour when switching between solutions. Why?
When loading a solution containing SpecFlow+, Visual Studio caches the SpecFlow+ components. If you open a new solution containing a SpecFlow+ project, Visual Studio will retain the cached version of the SpecFlow+ components in memory. If the version used by the two projects is different, this means that there will be a version mismatch.

You can avoid this issue by either upgrading all your solutions to the same version of SpecFlow+, or by restarting Visual Studio to flush the cache before opening the new solution.
