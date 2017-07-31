Generating living documentation from your Gherkin files with SpecFlow+ LivingDoc requires you to add the SpecFlow+ build step to your build process. This build step parses the Gherkin files in your solution and formats them for display in VSTS. 
A default build step is included when installing the extension. This build step only generates the documentation; it does not execute any tests or build your solution.

**Note:** You do not need to use TFS to actually build your application. You can simply add a build definition that acquires the sources and generates the documentation.


To add the build step:  

1. Select **Build & Release | Builds** from the menu in TFS
1. Click on build in the list (or add a new one).
1. On the **Summary** page, click on a recently completed build:  
  ![Build Summary](http://www.specflow.org/screenshots/Build_Summary.png) 
1. The build steps are displayed in the left in the next screen:  
  ![Build Steps](http://www.specflow.org/screenshots/Build_Steps.png)
1. Click on **Edit build definition** to edit the steps.
1. Add the SpecFlow+ build step to your build to generate the living documentation.
1. Enter the path to your project file in the **Project** file path field of the **SpecFlow+ build step** and make sure the step is enabled.
1. If you want to include Gherkin files from multiple projects, add a separate build step for each of your projects.  
  ![SpecFlow Step](http://www.specflow.org/screenshots/Build_SpecFlow_Step.png)
  

To generate the documentation:

1. Select **Test | SpecFlow+** from the menu.
1. Choose the build definition containing the SpecFlow+ build step(s).  
  ![Build Summary](http://www.specflow.org/screenshots/Choose_Build.png)
1. Click on **Queue build**. The build is added to the queue.
1. Once the build has completed, select **Test | SpecFlow+** from the menu to access the feature files.