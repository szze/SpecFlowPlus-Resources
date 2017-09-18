You can include markdown code in your feature files, and use markdown to embed images in your feature files. These images will then be displayed when viewing the feature file in TFS/VSTS.
**Note: Markdown is only supported in Feature and Scenario descriptions.** This means you can only place markdown between the "Feature:" row and the first scenario, or between the "Scenario:" row and the first step definition. If you place markdown elsewhere, you will receive errors when building the documentation.


## Embedding Images
When embedding images, the path to the image can be specified as a relative or absolute path. You can also embed images stored externally, such as on a website. Paths are relative to the location of the feature file.

**Embedding an image in the same directory as the feature file**

`![Alt text](image.png)`

**Embedding an image in a sub-directory**

`![Alt text](folder/image.png)`

**Embedding an image with an absolute reference**

`![Alt text](/folder/image.png)`

**Embedding an image relative to the parent directory**

`![Alt text](../image.png)`

**Embedding an external image**

`![Alt text](HTTPS://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQyBVE0UKugTT3yaJZ7fpr1nVK_RC9R5853AodqdLWMcsDl4PQw)`

### Example

The following code contains a link to an image in in the Feature description:

```
Feature: Everybody on the same page
![Swing](http://specflow.org/wp-content/uploads/2017/09/swing-sm.png)
	In order to ensure our software is fit-for-purpose
	As a conscientious software developer
	I want toshare specifications with all stakeholders

@mytag
Scenario: Embed image
	Given I have added an embedded image to my feature file using markdown
	When I view the resulting living documentation SpecFlow+LivingDoc 
	Then I see the image embedded inline
```

This is the resulting output in SpecFlow+ LivingDoc:

![Image in Gherkin](http://specflow.org/wp-content/uploads/2017/09/image-in-markdown.png)