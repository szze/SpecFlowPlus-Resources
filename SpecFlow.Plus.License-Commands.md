SpecFlow.Plus.License is used to register/unregister your license and display information on your current license. Information on installing the licensing tool can be found [[here|SpecFlowPlus Licensing]].

SpecFlow.Plus.License uses the [[getopt syntax|https://en.m.wikipedia.org/wiki/Getopt]]. Options need to be specified with a double dash before the option, e.g. `specflow-plus-license register --help` displays the help for the `register` command.

# Commands

## register

This command registers a license key for the current Windows user.

### Syntax

`specflow-plus-license register <LicenseKey> <IssuedTo> <options>`

The license key and licensee (issued to) are required to register a license. You will receive the license key and issued to value when purchasing a SpecFlow+ license. **Please keep the email with your license details in case you need to register the license again on a different machine!**

**Note:** If the licensee contains a space, make sure to enclose it in quotes.

**Example:**

`specflow-plus-license register ABCDEFG123 "John Doe"`

The following additional options are available:

**help**: Displays the help information for  the `register` command.  
**version**: Displays the assembly version information.


### Migrating Previous Licenses

Prior to SpecFlow 3, license keys were stored in the registry. However the .NET Core licensing tool cannot access licenses stored in the registry. If you intend to use SpecFlow+ with .NET Core and have already registered your license key, you can migrate your old key using the following command:
`specrun migrate-license`

This will copy your existing license from the registry to a local file that can be read by the .NET Core licensing tool.

## unregister

This command removes the license registered to the current Windows user.

### Syntax

`specflow-plus-license unregister`

The following additional options are available:

**help**: Displays the help information for  the `register` command.
**version**: Displays the assembly version information.

## about

This command displays information about the license registered on the current machine, as well as information on the version of the licensing tool.

### Syntax

`specflow-plus-license about <options>`

The following additional options are available:

**help**: Displays the help information for  the `register` command.
**version**: Displays the assembly version information.

### Sample Output

```
********************************
*** SpecFlow+ Licensing Tool ***
********************************

Version 1.8.5+g20ae9ada16
Assembly Version 1.8.0.0
Released 2015-03-03

Copyright c 2011-2018 TechTalk
http://www.specflow.org/plus

Build date: 2015-03-03
The registered license is registered for John Doe and is will expire <expiration date>.
```


## version

This command displays the assembly's version information.

### Syntax

`specflow-plus-license version`

## help

This command displays the help information for a command.

### Syntax

`specflow-plus-license help <command>`


The command is optional; if no command is specified, the help information for all commands is displayed.




