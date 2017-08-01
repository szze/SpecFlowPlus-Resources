The `<TestThreads>` element is a container for `<TestThread>` elements. The following attributes are available for `<TestThread>` elements: 


|Element/Attribute  |Required/Optional|Description|
|-------------------|-----------------|-----------|
|id               |     |Integer ID of the test thread (zero-indexed). This value can be accessed using the `{TestThreadId}` placholder. |
|TestAffinity       |Optional         | Defines a filter applied to tests run in this thread. Only tests containing with the specified tag are executed in the thread.<br>**Example:** `<TestAffinity>testpath:Target:FireFox</TestAffinity>` only executes tests with the `FireFox` tag in the thread.|

You can use the `{TestThreadId}` as a placeholder to reference the thread ID, e.g. to transform the name of the database instance you are accessing based on the thread ID, ensuring that each thread accesses a separate instance of the database. This prevents the threads from conflicting with one another when accessing the database, as thread 0 may manipulate data that is required by thread 1 otherwise.