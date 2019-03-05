Detailed information on SpecFlow+ Licensing can be found [[here|https://specflow.org/plus/licensing/]]. This section covers the process of registering your SpecFlow+ license.

## SpecFlow.Plus.License

As of SpecFlow 3, licenses need to be registered using the SpecFlow.Plus.License tool. It is used to assign, remove and display the current licensing status of a machine.

### Setup

#### Prerequisites

SpecFlow.Plus.License requires the .NET Core SDK 2.1 or higher to be installed. Information on setting up the .NET Core SDK can be found in the [[official Microsoft guide|https://www.microsoft.com/net/download]].

#### Installing SpecFlow.Plus.License

To install SpecFlow.Plus.License:

1. Open a command prompt.
1. Run the following command:  
  `dotnet tool install --global SpecFlow.Plus.License`  
  **Note:** If you want to install a specific version, use the `--version` option to specify the desired version:  
  `dotnet tool install --global SpecFlow.Plus.License --version <desired version>`
1. You can test that the installation was successfull and display your license status using the following command:  
  `specflow-plus-license about`

#### Uninstalling SpecFlow.Plus.License

To uninstall SpecFlow.Plus.License:
1. Open a command prompt.
1. Run the following command:  
  `dotnet tool uninstall --global SpecFlow.Plus.License`

### Migrating Previous Licenses

Prior to SpecFlow 3, license keys were stored in the registry. However the .NET Core licensing tool cannot access licenses stored in the registry. If you intend to use SpecFlow+ with .NET Core and have already registered your license key, you can migrate your old key using the following command:
`specrun migrate-license`

This will copy your existing license from the registry to a local file that can be read by the .NET Core licensing tool.