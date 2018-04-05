The `<VSTest>` element determines the behaviour when using SpecFlow+ Runner in conjunction with VS Test.


|Attribute         |Description|
|------------------|-----------|
|TestRetryResults  |By default, a test that initially fails is treated as having failed, even if the retries are successful. This can result in test execution results that show the same test as both failing (the initial test) and passing (the subsequent retries). This is particularly common when testing web applications if the initial test times out. In some cases, you may want to determine that a test should be treated as passing, even if one or other of the tests fails, allowing you to discount tests that time out.<br>The following options are available:<br>`Separate` (default): When retrying tests, separate test results are output for each execution of the test: the initial (failing) execution and all retries.<br>`Unified`: A single unified result is output for the test. If the percentage of successful tests (the initial test + all retries) exceeds the threshold (passRate), the test is treated as passing.|
|passRateRelative| Determines the percentage threshold (default = 100%) used to determine when a test should be treated as passing when using the `Unified` option. For example, if the `passRateRelative` is set to 50%, the test is only counted as passing if at least half the tests pass.|
|passRateAbsolute| Determines the number of successful retries to determine when a test should be treated as passing when using the `Unified` option. |

