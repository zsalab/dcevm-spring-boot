# IntelliJ Idea

## Review the problem

First let's try what would happen if we rename a controller method in a Spring Boot applcation.

You can check out this project and import to your IDE.

We should check our Java configuration, make sure OpenJDK is the project SDK.

![Configuration with OpenJDK](./ConfigureSDK-OpenJDK.png)

![Select SDK OpenJDK](./SelectSDK-OpenJDK.png)

We should make sure the auto build and code hotswap both enabled.

![Enable autobuild](./EnableAutoBuild.png)

![Enable hotswap](./EnableHotSwap.png)

*NOTE: by the time this manual written Idea does not do the auto build even it is enabled, you may build manually*

Start a debug session for the sample application, than open the `HelloController` class file.

![Start debug session](./StartDebugSession.png)

![Original code](./OriginalCode.png)

When you rename the `index()` method to for example `newIndex()` and save the file you will see this error:
_(Remember: you may build manually if your Idea does not support autobuild)_

![Rename method problem](./RenameMethodProblem.png)

You would see the same error when you delete any method (rename is a delete and an add operation)
Not much better if you try to add a new method without change anything else in the existing code.
_(Remember: you may build manually if your Idea does not support autobuild)_

![Add method problem](./AddMethodProblem.png)

Not really developer friendly solution. You can always restart your application in this case, but that is
really inefficient way of working especially if you have 5-20 sec startup time.

Stop the debug session and....

## Try DCEVM

Install DCEVM to your computer if you have not done yet.
[https://github.com/TravaOpenJDK/trava-jdk-11-dcevm/releases](https://github.com/TravaOpenJDK/trava-jdk-11-dcevm/releases)

We just have to change the project runtime VM and add the `-XX:HotswapAgent=` VM argument for the launch config.

Add DCEVM as a new SDK

![Configuration with OpenJDK](./ConfigureSDK-DCEVM.png)

One more step, we have change the debug configuration to switch DCEVM and enable the Hotswap Agent.

![Switch to DCEVM 1](./SwitchToDCEVM-1.png)

![Switch to DCEVM 2](./SwitchToDCEVM-2.png)

![Switch to DCEVM 3](./SwitchToDCEVM-3.png)

We can start our debug session with DCEVM and try to apply the changes again.

![Hotswap agent initialized](./HotswapAgentPluginsInitialized.png)

You can see in your terminal window something going on, the plugins needed for your code detected and initialized without any further configuration.

We can change the code now...

![Modified code](./ModifiedCode.png)

No complain about the unsupported hotswap operation after save the file. You will see in the terminal window the hotswap agent did some magic.

![Hot code replacement](./HotCodeReplacement.png)

You can try to fetch the other method with `curl http://localhost:8080/other`, you will get the expected response.
We see the new method works as it was always be there, lets remove it and call `curl http://localhost:8080/other` as we expect the response is 404 Not Found error.
_(Remember: you may build manually if your Idea does not support autobuild)_

Good work!