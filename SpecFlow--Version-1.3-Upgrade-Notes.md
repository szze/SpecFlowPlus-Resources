<p><b><i>Note: If you haven't already, please read the information on <a href="http://www.specflow.org/updating-to-specflow-2/">upgrading to SpecFlow 2</a></i></b>.</p>

<h1>Customised Report Templates</h1>

<h2>New Razor Engine and Syntax</h2>
<p>SpecFlow+ Runner 1.3 uses Razor 3.6.1, whereas the previous version used Razor 2.1.0. If you have created a custom report template, you may need to update your template to reflect the 3.6.1 syntax.</p>

<h2>Intellisense</h2>
Using intellisense with report templates requires a number of DLLs to be added as references to your project:
<ul>
<li>RazorEngine.dll</li>
<li>System.Web.Razor.dll</li>
<li>TechTalk.SpecRun.Framework.dll</li>
<li>TechTalk.SpecRun.Framework.Interfaces.dll</li>
</ul>

These DLLs are included in the NuGet package, but will not be updated to the new version when updating SpecFlow+ Runner to 1.3. You need to manually replace the old 1.2 versions of these DLLs with the versions in the 1.3 package.

<h1>Team Foundation Server XAML Build Agents</h1>
Different SpecFlow+ Runner versions require a different TFS XAML build agent. If you are using TFS XAML build agents with SpecFlow+ Runner and have projects with version 1.2 and projects with version 1.3, you need to ensure that these projects use the appropriate build agent. You can do this by defining tags to differentiate between the two versions.

To do so:
<ol>
<li>Open the Team Explorer in Visual Studio.<br><img src="http://www.specflow.org/media/Team-Explorer.png"></li>
<li>Click on <b>Builds</b>.</li>
<li>Right click on your build definition and select <b>Edit Build Definition</b>.</li>
<li>Click on <b>Process</b> in the pane on the left.</li>
<li>Open the <b>Advanced | Agent Settings</b> node.</li>
<li>Enter a suitable <b>Tags filter</b>, e.g. "SpecFlow+ Runner 1.2" or "SpecFlow+ Runner 1.3".<br><img src="http://www.specflow.org/media/Tag-Filter.png"></li>
<li>Open the TFS Server Administration Console on your build sever. Click on <b>Properties</b> next to the desired build agent and enter the same tag filter as before to assign the desired build agent.<br><img src="http://www.specflow.org/media/TFS-XAML-build.png"></li>
</ol>