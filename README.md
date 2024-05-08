# 1.2. Understanding how it works.

![test](image/ss1.png)

The Rust code does a few things. It compiles and runs first. Then, it sets up an executor and a spawner for tasks that happen at different times. One task prints "howdy!" and then waits for two seconds before printing "done!". This task runs alongside other tasks. Right after this task starts, a synchronous print statement "hey hey" runs. It happens before the other tasks in the queue, so "hey hey" gets printed first. After the wait, the asynchronous task continues, printing "howdy!" and "done!". This shows how Rust can handle different tasks happening at the same time, some synchronous and some asynchronous.


# 1.3. Multiple Spawn and removing drop

![test](image/ss2.png)

The updated Rust code shows how multiple tasks can happen at the same time, each waiting for two seconds. When I run the code, "howdy", "howdy2", and "howdy3" printed, followed by "done" for each. This happens because each task starts independently in the executor. In this version, not calling `drop(spawner)` means the executor doesn't stop, potentially running forever if new tasks are added. But in the code, all tasks finish because I start the executor after all tasks are added. This demonstrates how Rust handles many tasks at once and managing them well through the executor and task queue. Each task waits for two seconds because of the `TimerFuture` and then continues and finishes by printing "done".
