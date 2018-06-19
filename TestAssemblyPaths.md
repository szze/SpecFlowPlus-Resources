The `<TestAssemblyPaths>` element is a container for `<TestAssemblyPath>` elements, which define your assembly paths when executing tests from the command line. Paths in `<TestAssemblyPath>` elements are relative to the base folder.

**Make sure that you specify the correct name(s) of all your assembly file(s) in their own `<TestAssemblyPath>` element, otherwise no tests will be found!**

**Example:** 
```xml
<TestAssemblyPaths>
    <TestAssemblyPath>SpecRun.TestProject.dll</TestAssemblyPath>
</TestAssemblyPaths>
```