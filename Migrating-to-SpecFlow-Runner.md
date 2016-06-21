SpecFlow+ Runner works with any assertions API, which means that switching from another test runner to SpecFlow+ Runner is easy. To switch, you will need to:

1. Install a NuGet package.
1. Configure your [unitTestProvider](http://www.specflow.org/documentation/Configuration/) for SpecFlow+ Runner.
1. Regenerate your feature files.

Once you have completed these steps, you can run your tests with SpecFlow+Runner. More detailed information on the steps necessary for different unit test providers are provided below.

#Detailed steps

##MSTest
1. Remove the `SpecFlow.MsTest` NuGet package from your project, if present.
1. Add the `SpecRun.SpecFlow` NuGet package to your project.
1. Update the `unitTestProvider` element in your `app.config` file as follows:

  ```xml
  <specFlow>
      <unitTestProvider name="SpecRun" /> 
      <plugins>
          <add name="SpecRun" />
      </plugins>
  </specFlow>
  ```

1. Right-click on your specifications project in the Solution Explorer, and select **Regenerate Feature Files** from the menu to regenerate the feature files.

##NUnit 2 & NUnit 3
1. Add the `SpecRun.SpecFlow` NuGet package to your project.
1. Update the `unitTestProvider` element in your `app.config` file, which may contain multiple `unitTestProvider` entries:

  ```xml
  <specFlow>
      <unitTestProvider name="SpecRun" />
      <plugins>
          <add name="SpecRun" />
      </plugins>
  </specFlow>
```

1. Right-click on your specifications project in the Solution Explorer, and select **Regenerate Feature Files** from the menu to regenerate the feature files.

#XUnit
1. Add the `SpecRun.SpecFlow` NuGet package to your project.
1. Update the `unitTestProvider` element in your `app.config` file, which may contain multiple `unitTestProvider` entries:
  
  ```xml
  <specFlow>
      <unitTestProvider name="SpecRun" /> 
      <plugins>
          <add name="SpecRun" />
      </plugins>
  </specFlow>
  ```

1. Right-click on your specifications project in the Solution Explorer, and select **Regenerate Feature Files** from the menu to regenerate the feature files.