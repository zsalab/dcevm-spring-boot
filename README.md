# Extended Java HotSwap capabilities

You most likely frustrated when you work with Java and try to code on the fly. When you change a method body the
JVM hotswap works well, but if you change the structure of your class you get the error message as the hotswap failed.
Standard JVM unfortunately has limited hotswap capability.
There is couple of solution to improve this situation, like JRebel, Spring Loaded, and HotSwap Project with DCEVM.
This manual introduct the HotSwap Project with DCEVM.
Spring Loaded fails many times and not really maintained any more.
JRebel works on any standard VM, other hand you need some plugin for your IDE and magic to integrate with it. Further more it is expensive.

HotSwap Project with DCEVM need no more configuration or IDE plugin then chose the right VM and execute with `-XX:HotswapAgent=` argument.

## Features

_In contrast to standard Java, where the hotswap is limited to in-body code changes, the DCEVM + HotswapAgent allow following code changes:_

- _Add/remove/modify class fields._
- _Add/remove/modify methods. Add/remove/modify method annotations_
- _Add/remove/modify classes including anonymous classes. HotswapAgent handless correct anonymous class redefinitions._
- _Add/remove static member of classes. HotswapAgent handles static member initialization._
- _Add/remove enum values_
- _Refresh framework and application server settings_

_The only unsupported operation is hierarchy change (change the superclass or remove an interface)._

_DCEVM realizes hotswap on JVM level. HotwapAgent does the same on level of Java frameworks and servlet containers. Both projects used together forms excellent combination for daily development not only in Java but also in another JVM languages._

Quoted from the project [website](http://hotswapagent.org/index.html)

## Framework compatibility

DCEVM provide the additional hotswap capabilities to the JVM, but that would not help you with the frameworks having internal state like injected beans and other configurations.
The HotSwapAgent do this job, it comes with many plugins for support of different frameworks. You can also extend it with your custom plugin if it is needed.

Many plugins already exists and packaged into DCEVM like Spring, Hibernate, Vaadin, Weld, Tomcat, Undertow, Jetty, Jersey, Log4j, etc.

Take a look on the [website](http://hotswapagent.org/index.html) for the existing plugins.

## IDE configurations

Generaly speaking you do not need any IDE plugins for make the magic happen.

[Visual Studio Code / Theia](./IDEs/TheiaVSC/README.md)

[Eclipse](./IDEs/Eclipse/README.md)

[IntelliJ Idea](./IDEs/IntelliJ/README.md)

Note: You can find configuration HOWTOs on the project [website](http://hotswapagent.org/index.html), may different than in this manual.
