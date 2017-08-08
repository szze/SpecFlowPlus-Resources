The following are known issues with SpecFlow+, and are scheduled to be fixed:

* "Object reference not set to an instance of an object" when using NUnit's Assert command in conjunction with NUnit tests executed with SpecFlow+ Runner. This appears to be due to a recent update to NUnit (possibly 3.6.1). See [[this GitHub issue|https://github.com/nunit/nunit/issues/2223]].
* Tests fail to execute if the path to the project includes a hash character ('#')