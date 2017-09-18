You can use markdown code to embed images in your feature files. These images will then be displayed when viewing the feature file in TFS/VSTS.
**Note: Markdown is only supported in Feature and Scenario descriptions.** This means you can only place markdown between the "Feature:" row and the first scenario, or between the "Scenario:" row and the first step definition. If you place markdown elsewhere, you will receive errors when building the documentation.

When embedding images, the path to the image can be specified as a relative or absolute path. You can also embed images stored externally, such as on a website. Paths are relative to the location of the feature file.

Examples:

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
