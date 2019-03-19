To add the build step in TFS/VSTS/DevOps:  

1. Select **Build & Release | Builds** from the menu in TFS
1. Click on build in the list (or add a new one).
1. On the **Summary** page, click on a recently completed build:  
  ![Build Summary](http://www.specflow.org/screenshots/Build_Summary.png) 
1. The build steps are displayed in the left in the next screen:  
  ![Build Steps](http://www.specflow.org/screenshots/Build_Steps.png)
1. Click on **Edit build definition** to edit the steps.
1. Add the SpecFlow+ build step to your build to generate the living documentation.
1. Enter the path to your project (.csproj file) or the folder containing your project in the **Project file path** field in the **SpecFlow+ build step** and make sure the step is enabled. All feature files in the selected folder and all its sub-folders are included in your living documentation.
If you have not referenced a .csproj file and you are not using English as the default language of your Gherkin files, select the language used by your Gherkin files under **Project Language**. (If you have referenced a .csproj file, this information is read from the app.config file.)
1. You can also enter a **Project Name**. This name is used by the root node in the tree. If you do not enter a name here, the name of the Visual Studio project is used instead.
1. If you want to include Gherkin files from multiple projects, add a separate build step for each of your projects.  
  ![SpecFlow Step](http://www.specflow.org/screenshots/Build_SpecFlow_Step.png)