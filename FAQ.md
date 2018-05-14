***Note:*** *Don't forget to check out the [[SpecFlow FAQ|http://www.specflow.org/documentation/FAQ/]] as well.*

Information on our privacy policy and the information we collect from customers can be found [[here|https://www.specflow.org/privacy-policy/]].

<h1 id="Licensing">Licensing</h1>

## How is SpecFlow+ licensed?
SpecFlow+ is licensed per user. A single license entitles a single user to execute tests with SpecFlow+ on any number of local or remote machines (including build servers). Build servers do not require a separate license. Each user who triggers builds that involve SpecFlow+ either locally or on a build server (e.g. through checking in a Gherkin file) requires a license. Users of the LivingDoc VSTS plugin require a license as well.

More details on SpecFlow+ licensing (including academic/non-profit licenses) can be found [[here|http://www.specflow.org/plus/licensing/]].

## Are SpecFlow+ licenses perpetual or subscription based?

SpecFlow+ licenses are perpetual licenses that include 1 year of upgrades and support. Your license key will unlock all versions of SpecFlow+ released during this 1 year period, as well as any earlier versions. Once the 1-year period is over, the license key will continue to unlock older versions (i.e. those released prior to the end of the upgrade period), but will not unlock versions released after this 1-year period is over. 

You can extend your license period for another year at 50% of the original license fee. Extensions are always from the end of the previous support period.

## What support is included during the support period?
In addition to having access to the latest releases and pre-releases, we provide support for technical issues during the support period. We will attempt to fix all bugs that are reported, and will prioritise these bugs according to their severity. 

## What level of TFS/VSTS user is required to use SpecFlow+ LivingDoc?
Any level except from "Stakeholder" works with SpecFlow+ LivingDoc. Stakeholders are unable to access the "Test" menu, which provides access to SpecFlow+ LivingDoc.


## How do I register my license for SpecFlow+?
You need to register your license key once per machine (after adding SpecFlow+ to your first project). More information is available [[here|http://www.specflow.org/plus/evaluation/]] and [[here|http://www.specflow.org/plus/documentation/SpecFlowPlus-Excel-Command-Line-Tool-Reference/]].

<h1 id="Sales">Sales and Pricing</h1>

## How much does a SpecFlow+ license cost?

The list price for a single user is EUR 159. This includes 1 year of upgrades and support. We can provide you with a quote in GBP or USD if you prefer. In this case, we use the current exchange rate to set the price, which is fixed for 30 days. This means the price is unaffected by any subsequent changes in the exchange rate. 

## How can I order SpecFlow+
If you are ordering less than 5 licenses, we recommend purchasing from the [[web shop|https://www.swreg.org/com/shop/138662/cart/7886888002]].

If you are ordering 5 or more licenses, please contact us directly at _support [at] specflow.org_, and include us the number of licenses you are interested in and your preferred currency (EUR/USD/GBP). We will send you a quote.

## Are bulk discounts available?

We can offer discounts on larger orders (5+), with the discount depending on the number of licenses. Please contact us at support [at] specflow.org for a quote. 

## How can I complete payment?
You can choose a number of payment options when purchasing from the [[web shop|https://www.swreg.org/com/shop/138662/cart/7886888002]]. 
When ordering directly from TechTalk (via support [at] specflow.org), payment by credit card is preferred. If you accept the quote, we will send you a payment link. Payment by bank transfer is also possible, but is much slower to process.

**We cannot send out license keys until payment is confirmed!**

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

<h1 id="Advantages">What are the advantages of SpecFlow+ Runner</h1>

SpecFlow+ Runner offers a number of features that go beyond those found in other test runners. A comparison of the advantages of SpecFlow+ over SpecFlow can be found [[here|http://specflow.org/plus/]].

Some of the key features of SpecFlow+ Runner are:  

* Support for multiple [[targets]], allowing you to write a single test to target different [[environments|Environment]] (e.g. x86 and x64, various browsers).
* [[Configuration file transformations|DeploymentTransformation]], which can also be used in conjunction with targets. This allows you to transform your configuration file for different platforms or web browsers, or set up a separate database instance for each thread using [[placeholders]].
* Advanced reporting options using CSHTML templates. You can configure the output to meet your specific needs, both by customising the formatting and determining which data to include and how it should be laid out. 3 default templates are included to get you started that output your test reports as either HTML, JSON or XML.
* Adaptive test scheduling mode prioritises previously failing tests over stable tests based on your execution history. Note that this feature requires you to set up a [[SpecFlow+ Runner server|Setting-up-the-SpecFlowPlus-Runner-Server]].
* Parallelisation and isolation options for multi-threaded test execution. You can isolate threads by AppDomain, SharedAppDomain or Process.


<h1 id="upgrades">Upgrading</h1>

### I am having trouble upgrading from SpecFlow+ 1.3 (or earlier) to a newer version with SpecFlow 2 support
Make sure you follow the steps out lined in the guide on [[updating to SpecFlow 2|http://www.specflow.org/updating-to-specflow-2/]].  
In particular:  

* Make sure you restart Visual Studio as described in the link! You need to do this to flush Visual Studio's cache and ensure the correct version of SpecFlow+ is loaded.
* If you use Visual Studio 2013 (or earlier) make sure you have removed any references to older versions of SpecFlow+ from you 'packages.config' file.

### I have multiple solutions with different versions of SpecFlow+ installed and am observing weird behaviour when switching between solutions. Why?
When loading a solution containing SpecFlow+, Visual Studio caches the SpecFlow+ components. If you open a new solution containing a SpecFlow+ project, Visual Studio will retain the cached version of the SpecFlow+ components in memory. If the version used by the two projects is different, this means that there will be a version mismatch.

You can avoid this issue by either upgrading all your solutions to the same version of SpecFlow+, or by restarting Visual Studio to flush the cache before opening the new solution.

<h1 id="Support">Support</h1>

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

<h1 id="Misc">Miscellaneous</h1>

### Do you use SpecFlow+ to develop SpecFlow+?
Yes!