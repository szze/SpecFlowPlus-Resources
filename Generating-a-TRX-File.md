To generate a TRX file with SpecFlow+ Runner, you will need to start your tests from the command line using `vstest.console.exe`. You will need to specify the path to `specrun.exe` (the test adapter path), and use the `/logger:trx` option to generate a TRX file.

Execute your tests using the following syntax:
`vstest.console.exe <MyTestAssembly.dll> /TestAdapterPath:<PATH_TO_SPECRUN.EXE> /logger:trx`

Replace `<MyTestAssembly.dll>` and `<PATH_TO_SPECRUN.EXE>` with the name of your test assembly and the path to `specrun.exe` (located in the `/packages/specrun<version>/tools` directory of your project).

