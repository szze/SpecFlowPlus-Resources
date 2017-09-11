Once you have [[generated your documentation|Generating-Documentation]] using the SpecFlow+ build step, select **Test|SpecFlow+** from the menu in TFS to view the most recent state of the documentation.

XXX SCREENSHOT XXX


## Switching to Related Feature Files (TFS/VSTS repositories only)
If your source code (feature files) is stored in a TFS/VSTS repository, you can switch directly from the living documentation to the source feature files. You can then edit the feature files directly in TFS/VSTS.


To switch to a feature file:  
1. Open the corresponding page in the living documentation.
1. Click on **Show source** at the top of the page.  
  **Note:** If your feature files are stored in a source other than TFS/VSTS, clicking on the link will result in an error (400: bad request). This feature only works in conjunction with the "This project" source option. 
1. The corresponding source feature file in your code repository is opened. You can edit the file directly in TFS/VSTS.

**Note:** Editing the feature files uses the standard TFS/VSTS interface, and you may need to merge any conflicts that arise from your edits.