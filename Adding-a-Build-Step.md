Generating living documentation from your Gherkin files with SpecFlow+ LivingDoc requires you to add the SpecFlow+ build step to your build process. This build step parses the Gherkin files in your solution and formats them for display in DevOps/VSTS/TFS. 

A default build step for is included when installing the extension. **This build step only generates the documentation; it does not execute any tests or build your solution.** 

For more information on configuring the build step, see the appropriate chapter depending on the type of build:  
* Build step configured in DevOps/TFS/VSTS: See [[Configuring-the-Build-Step-in-DevOps]]
* YAML build step: See [[Configuring the Build Step in YAML]]

**Note:** You do not need to use TFS to actually build your application. You can simply add a build definition that acquires the sources and generates the documentation.