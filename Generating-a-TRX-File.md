To generate a TRX file with SpecFlow+ Runner, you will need to start your tests from the command line using `vstest.console.exe` with the `/logger:trx` option to generate a TRX file.

You have to execute it in the output folder of your test project (`bin\debug\`).

### SpecFlow+Runner 1.8 and Later

Execute your tests using the following syntax:  
`vstest.console.exe <MyTestAssembly.dll> /logger:trx`

### Before SpecFlow+Runner 1.8

You have to specify the path to the testadapter, so you execute your tests using the following syntax:  
`vstest.console.exe <MyTestAssembly.dll> /TestAdapterPath:<PATH_TO_TESTADAPTER.EXE> /logger:trx`

Replace `<MyTestAssembly.dll>` with the name of your test assembly.  
<PATH_TO_TESTADAPTER.EXE> is the path to the `TechTalk.SpecRun.VisualStudio.TestAdapter.dll` (located in the `/packages/specrun<version>/tools` directory of your project).

