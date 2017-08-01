SpecFlow+ Runner profiles (`.srprofile` file extension) are XML files that determine how SpecFlow+ Runner executes your tests. This includes the behaviour when tests fail (e.g. repeat the test, abort after X failed tests), defining various target environments for your tests (e.g. different web browsers or x64/x86), enabling multi-threading, configuring folder and file paths and applying transformations to your default configuration file in order to change the transform the configuration file for different target environments. 

A file named `Default.srprofile` is automatically added to your Visual Studio project when you add the NuGet package to your solution. This profile is relatively basic, and includes your project name, ID and various default settings. It also includes a commented out section that you can use to transform the database connection string in your configuration file in order to access a different database instance. 

The name of the profile file used by your project is defined using the `<Profile>` tag in your `.runsettings` file.

# SpecFlow+ Runner Profile Elements and Attributes

The `<TestProfile>` element is a container for the remaining elements.

The following XML elements and attributes are available:
* [[&lt;Settings>|Settings]]
* [[&lt;Server>|Server]]
* [[&lt;Execution>|Execution]]
* [[&lt;Environment>|Environment]]
* [[&lt;TestAssemblyPaths>|TestAssemblyPaths]]
* [[&lt;Filter>|Filter]]
* [[&lt;Targets>|Targets]]
* [[&lt;DeploymentTransformation>|DeploymentTransformation]]
* [[&lt;TestThreads>|TestThreads]]
* [[&lt;Report>|Report]]

You can also use a number of [[Placeholders]] in your profile.
