SpecFlow+ LivingDoc uses the same licensing mechanism as the other SpecFlow+ components. If you have purchased SpecFlow+, your license key will also unlock SpecFlow+ LivingDoc.

## Restrictions in Evaluation Mode
If you have not registered a license key, SpecFlow+ LivingDoc runs in evaluation mode. This is indicated by the "evaluation mode" hint at the top right of the screen.

When running in evaluation mode, only the first 10 documentation entries can be viewed.

## Registering Your License
Once you have [[generated your documentation|Generating-Documentation]] using the SpecFlow+ build step, you can access the output from the **Test** menu in TFS/VSTS. When viewing the output, your license details are displayed at the top right of the screen. If you have not yet registered your license, "evaluation mode" is displayed here.

To register your license:

1. Click on **evaluation mode** at the top right of the screen. A dialog is displayed: 
  ![License Dialog](http://www.specflow.org/screenshots/License_dialog.png)
1. Enter your license details in the dialog. If you purchased SpecFlow+ via SWREG, the **IssuedTo** value is the email used to complete the purchase. If you purchased the license directly from TechTalk, you should have received an email containing both the licensee (**IssuedTo**) and license key.
1. Click on **Update**.
1. If your license data is correct, the dialog is closed. The licensing information at the top right of the screen is updated to show the licensee:  
  ![Successful Registration](http://www.specflow.org/screenshots/successfully_registered.png)

## License Information
After registering your SpecFlow+ license, you can hover over the "issued to: &lt;Licensee>" text to display additional information on your license:  
![License Details](http://www.specflow.org/screenshots/License_details.png)
* **canUpdateUntil**: This date is indicates the end of your current support period. This is normally one year after the date of purchase. XXX WHAT HAPPENS WHEN THIS DATE IS REACHED IF THE APP UPDATES ITSELF??? XXX
* **expirationDate**: This date indicates when your license expires, at which point you will no longer be able to use SpecFlow+ (except in evalution mode). **Most licenses do not have an expiration date**, in which case this value is empty.

XXX VERSION MISSING XXX

## Unregistering Your License
To unregister your license:  
1. Click on the "issued to: &lt;Licensee>" text at the top right. A dialog is opened.
2. Leave the **Key** field empty and click on **Update**.
3. The dialog is closed and the license information at the top right reverts back to "evaluation mode".