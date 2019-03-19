Once you have [[generated your documentation|Generating-Documentation]] using the SpecFlow+ build step, select **Test Plans |SpecFlow+** (DevOps) or **Test | SpecFlow+** (TFS/VSTS) from the menu to view the most recent state of the documentation.

![Sample Output](http://www.specflow.org/screenshots/sample_dox.png)

The tree on the left contains depicts the structure of your specifications. Blue entries represent features and scenarios. Black entries are based on the file structure of your project.

Click on a scenario or feature (blue text) in the tree to display the documentation generated for that scenario or feature in the area on the right.

The date of the latest build is displayed at the top. If subsequent builds have failed, the most recent failed build is also displayed. If a build is currently in progress, this information is also displayed.

## Switching to Related Feature Files
If your source code (feature files) is stored in a TFS/VSTS or GitHub repository, you can switch directly from the living documentation to the source feature files. You can then edit the feature files directly in TFS/VSTS or on GitHub.


To switch to a feature file:  

1. Open the corresponding page in the living documentation.
1. Click on **Show source** at the top of the page.  
  **Note:** If your feature files are stored in a source other than TFS/VSTS or GitHub, this option is not available. 
1. The corresponding source feature file in your code repository is opened. You can edit the file directly in TFS/VSTS or GitHub.  
  **Note:** You may need to merge any conflicts that arise from your edits.