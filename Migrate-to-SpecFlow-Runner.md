Switching from any test runner to SpecFlow+Runner is easy, because it works with any Assertions APIs.  
You simply need to install a NuGet package and check your [unitTestProvider](http://www.specflow.org/documentation/Configuration/) configuration of SpecFlow.  
After you have regenerated your feature files, you can run your tests with SpecFlow+Runner.


#Detailed steps

##MSTest
1.) Remove the NuGet package _SpecFlow.MsTest_, if it is existing  
2.) Add NuGet package _SpecRun.SpecFlow_  
3.) Check that you have following unitTestProvider configuration in your app.config  
```xml
<specFlow>
    <unitTestProvider name="SpecRun" /> 
    <plugins>
        <add name="SpecRun" />
    </plugins>
</specFlow>
```
4.) regenerate your feature files

##NUnit 2 & NUnit 3
1.) Add NuGet package _SpecRun.SpecFlow_  
2.) Fix your unitTestProvider configuration in your app.config.  
Propably you will have multiple unitTestProvider entries.
  
```xml
<specFlow>
    <unitTestProvider name="SpecRun" /> 
    <plugins>
        <add name="SpecRun" />
    </plugins>
</specFlow>
```
3.) regenerate your feature files

#XUnit
1.) Add NuGet package _SpecRun.SpecFlow_  
2.) Fix your unitTestProvider configuration in your app.config.  
Propably you will have multiple unitTestProvider entries.
  
```xml
<specFlow>
    <unitTestProvider name="SpecRun" /> 
    <plugins>
        <add name="SpecRun" />
    </plugins>
</specFlow>
```
3.) regenerate your feature files