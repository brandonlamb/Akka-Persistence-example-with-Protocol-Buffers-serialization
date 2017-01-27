# Akka Persistence example with Protocol Buffers serialization

### Build Status
[![Build Status](https://travis-ci.org/calvinlfer/play-framework-validation-example.svg?branch=master)](https://travis-ci.org/calvinlfer/play-framework-validation-example)

### Overview 
This example uses [ScalaPB](https://trueaccord.github.io/ScalaPB/) in order to obtain case class support for Scala when
generating code from `*.proto` files. ScalaPB uses the `protoc-jar` internally to compile your protocol buffer files.

Execute `sbt run` in order to run the `Main` application. The `Calculator` actor is used to persist events across runs
using Event Sourcing. We define a custom serializer that makes use of the generated class' (from proto)
serialization mechanisms to easily serialize and deserialize events.

The `Main` application fires events at the `Calculator` actor. Since `Calculator` actor is Persistent, it makes use of
the Serializer (set up in `application.conf`) when reading and persistent events to/from the event journal.

We also have a [test](https://github.com/referentiallytransparent/Akka-Persistence-example-with-Protocol-Buffers-serialization/blob/master/src/test/scala/com/experiments/calculator/PersistentCalculatorSpec.scala) that exercises the Persistent `Calculator` Actor by sending it events, killing it and making sure it uses Event Sourcing to bring the `Calculator` up to the current state. You can use `sbt test` to run the test.
 
 If you are using IntelliJ and want syntax highlighting, then make sure your directory setup looks like this:
 ![image](https://cloud.githubusercontent.com/assets/14280155/14578746/e1a8e258-035e-11e6-86af-5a74669930d5.png)

### External Libraries ###
- [ScalaPB](https://trueaccord.github.io/ScalaPB/) is used to generate `Scala case classes` from `proto` files. These case classes have the ability to convert to and from binary
- [Akka](http://akka.io/) for its actor framework, persistence module and test kit

**Warning: Make sure you have Python 2.7 installed (accessible via `python`)** otherwise the protocol buffers compiler will give you errors and will not compile your project
