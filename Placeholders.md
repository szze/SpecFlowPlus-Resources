There are placeholders available for the elements defined in your profile. You can use these placeholders in your configuration file. This allows you to use the same configuration file for various target environments, e.g. you could use the `{TestThreadId}` placeholder in the name of your database instance to ensure that each thread accesses a different instance of your database (Instance0, Instance1 etc.) . 

The following placeholders are available:

* `{TestThreadId}`: The ID of the current thread (integer)
* `{Target}`: The name of the current target (string)
* `{UniqueId}`: The unique ID entered in the profile
* `{BaseFolder}`: The base folder
* `{OutputFolder}`: The output folder for test results and reports
* All environment variables (specified using the standard format, i.e. enclosed in percentage signs ('%'))

Placeholders can be used in the following elements:

* ConfigFileTransformation/Transformation 
* CopyFile/target
* CopyFile/source 
* CopyFile/targetFolder
* CopyFolder/source 
* CopyFolder/target 
* CustomDeploystep/type (in the assembly path) 
* IISExpress/Port 
* IISExpress/webAppFolder 
* IISExpress/iisExpressPath 
* RelocateConfigurationFile/target 
* Relocate/targetFolder