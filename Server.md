You can publish the results of your tests to a SpecFlow+ Runner server. Details on setting up the server can be found [[here|Setting-up-the-SpecFlowPlus-Runner-Server]].

The following attributes are available:

|Attribute     |Required/Optional|Description|
|--------------|-----------------|-----------|
|serverURL     |**Required**     |The full URL of the SpecFlow+ Runner server, including transfer protocol and port number (6365)|
|publishResults|Optional         |Determines whether the results are published to the server or not (default = false) 

**Example:**  
```xml
<Server serverUrl="http://specrun.server:6365" publishResults="true" />
```