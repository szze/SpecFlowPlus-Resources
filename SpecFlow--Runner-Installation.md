The components in SpecFlow+ are distributed as NuGet package. There is a separate package for SpecFlow+ Runner (SpecRun) and SpecFlow+ Excel. Both components require SpecFlow to be installed as well. SpecFlow is also available as a NuGet package of  its own, but installing one of the SpecFlow+ packages automatically installs the SpecFlow NuGet package as well.

The installation of SpecFlow and SpecFlow+ Runner is described in detail in the [[Getting Started|http://www.specflow.org/getting-started]] guide for SpecFlow. The installation of the SpecFlow components is also covered in the [[SpecFlow documentation|http://www.specflow.org/documentation/Installation/]]. 

Details on installing SpecFlow+ Excel can be found [[here|http://www.specflow.org/plus/documentation/SpecFlowPlus-Excel-Installation-and-Configuration/]].

<h2>Installation and Setup</h2>
Installing SpecFlow consists of two steps:
<ol>
	<li>Install the IDE integration</li>
	<li>Set up your Visual Studio project to work with SpecFlow</li>
</ol>

<h3>Installing the IDE Integration Packages</h3>
The method used to install the IDE Integration packages depends on your IDE:
<ul>
	<li><strong>Visual Studio 2010+ (including Community Edition but not Express Edition):</strong> The easiest method is to select <strong>Tools&nbsp;|&nbsp;Extensions and Updates</strong> from the menu in Visual Studio, switch to the <strong>Online</strong> search on the left and enter “SpecFlow” in the search field at the top right.<br>
<img src="http://www.specflow.org/media/ExtensionsAndUpdatesDialog.png" alt="ExtensionsAndUpdatesDialog" class="alignnone size-full wp-image-1037" />
</li>
	<li><strong>Visual Studio Express</strong>: Refer to <a href="http://www.specflow.org/documentation/Install-IDE-Integration/">Install IDE Integration</a> for direct download links and information on installing SpecFlow for other IDEs.</li>
</ul>

<h3>Setting Up your SpecFlow Project</h3>
<p>Once you have installed the Visual Studio integration, you need to set up your solution to use SpecFlow. SpecFlow tests are usually placed in separate projects in your solution. The quickest way to set up a project is add the NuGet package to your project. For a detailed project setup guide, see the <a href="http://www.specflow.org/documentation/Setup-SpecFlow-Projects/">Setup SpecFlow Projects</a> page.</p>

<p>To set up your specification project:</p>
<ol>
	<li>Add  "Unit Testing Project" to your solution (e.g. "MyProject.Specs").<br>
<strong>Note:</strong> Creating a “Unit Test Project” is the recommended procedure, as it reduces the number of steps required to set up your project.</li>
        <li>You can choose to remove the UnitTestX.cs file, as it is not required.</li>
	<li>Add SpecFlow+ Runner to your specification project using NuGet:
<ol>
	<li>Right-click on your specification project (e.g. “MyProject.Specs”) and select <strong>Manage NuGet Packages for Solution</strong>.</li>
	<li>Search for “SpecRun” and install <em>SpecRun for SpecFlow</em>. The latest version is installed automatically, although you can choose to install an earlier version if needed.
        <br>
        Alternatively, you can install the package from NuGet's console (<strong>Tools&nbsp;|&nbsp;NuGet Package Manager&nbsp;|&nbsp;Package Manager Console</strong>) as follows:<br>
<code>PM&gt; Install-Package SpecRun.SpecFlow</code></li>
</ol>
</li>
	Installing SpecFlow+ Runner automatically downloads the SpecFlow runtime from NuGet and adds it to your specifications project.
</ol>


<h2>Registering SpecFlow+</h2>
For details on registering SpecFlow+ Runner, see [[Registering SpecFlow+|Registering-SpecFlowPlus]]