SpecFlow+ LivingDoc parses your feature files looking for keywords, and uses these keywords to format the output. SpecFlow+ LivingDoc supports all languages supported by the official Gherkin parser.

The language used to parse the feature files is determined as follows:

* The default language is en-US.
* If you have entered a language in your [[app.config|http://specflow.org/documentation/Configuration/]] file, this language is used as the default language for all feature files.<br>
  **Note:** If you have only entered a folder in your **Project file path** in the build step, the settings in your app.config file are ignored. You need to enter the project file itself (.csproj) in order for SpecFlow+ LivingDoc to be able to determine the appropriate app.config file.
* The language entered in the Gherkin file (using `# language`) takes priority over the language in the app.config file. 