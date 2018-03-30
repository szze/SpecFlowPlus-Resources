The `<Filter>` element allows you to define filters that are applied to your tests, allowing you to determine which tests to execute. Filters can also be defined in `<Target>` elements, in which case the filter only applies to that target. Filters defined outside of a `<Target>` element are applied globally. The **Test Explorer** window in Visual Studio only lists those tests that meet your filter criteria (after rebuilding your project). Note that global filters also apply when running tests by right-clicking on a feature file and selecting **Run SpecFlow Scenarios**.

Filters can be applied to tests based on tags (including regular expressions), or the scenario or feature name.

**Note:** Tags and filters are **case-sensitive**.

The following filter types can be defined:

|Prefix    |Type      |Description|
|----------|----------|-----------|
|@         |Tag       |Matches a tag exactly, e.g. '@MyTag' only returns those tests with the '@MyTag' tag.|
|tagmatch: |Tag       |Matches tags by regular expression, e.g. 'tagmatch:Tag[1-3]' matches tests with the tags 'Tag1', "Tag2' or 'Tag3'.|
|testpath:Feature: |Test      |Matches tests by feature name. You can use the `*` wildcard in feature names, e.g. `testpath:"Feature:Calcu*"` matches the features "Calculator" and "Calculus".<br>**Note**: Replace spaces in scenario names with the plus character (+) in your filter. Example:<br>Replace `Buy a book` with `Buy+a+book`.|
|testpath:Scenario:|Test      |Matches tests by scenario name. You can use the `*` wildcard in scenario names, e.g. `testpath:"Scenario:*+two+numbers"` matches the scenarios "Add two numbers", "Subtract two numbers" and "Multiply two numbers".<br>**Note**: Replace spaces in scenario names with the plus character (+) in your filter. Example:<br>Replace `Buy a book` with `Buy+a+book`. |

You can combine filters using logical operators. The following operators are supported:  
<ul>
<li>|: OR</li>
<li>&amp;: AND (however you need to use <code>&amp;amp;</code> instead in the profile, as it is an XML file)</li>
<li>!: NOT</li>
</ul>

**Examples:**  
`<Filter>@MyTag &amp; @YourTag</Filter>` executes all tests with both the `@MyTag` and `@YourTag` tags.  
`<Filter>!tagmatch:Tag[1-9]</Filter>` executes all tests that are not tagged with any of  `@Tag1` to `@Tag9`.  
<`Filter>@MyTag | tagmatch:tag[1-9]</Filter>` executes all tests with either the `@MyTag` tag or tags `@Tag1` to `@Tag9`.