# Applications

## Introduction

How to deploy applications?
How to perform basic deployments?

### Programming Languages

Top languages from 2019
1. JS/Node.js
2. Python
3. Java

Types
1. Compiled
  - First developed, then compiled, then executed
2. Interpreted
  - Developed, executed
  - Implicitly compiled into bytecode

A compiler translates code into different languages.
- In the past, a program had to be compiled on different systems to run on different OSs.
- Now, converted to bytecode instead to be run on a virtual machine.
  - As long as a languages virtual machine is available on a system, it can be run.
  - This type of thing is done in the background.
Packages
- Bits of software to be used by developers as dependencies in their applications

Build
- Dev -> Build -> Test -> Deliver
  - Important to konw what to automate.

## Java

Many organization stuck at version 8
- Version 9 introduced breaking changes and licensing terms

### Retrieve java
```sh
wget https://download.java.net....
#=> openjdk-13.0.2_linux-x64_bin.tar.gz
tar -xzf openjdk-13.0.2_linux-x64_bin.tar.gz
#=> /opt/jdk-13/bin/java-version

# Check java version w/ java command
/jdk-13/bin/java -version

java version
```


Java Development Kit (JDK)
- Develop
- Build
- Run

### Building and running a Java application
- Compile w/ java compiler (i.e. `javac`)
- Run w/ `java` cmd

An archiver like JAR (Java Archive) help compile several packages into a single file.

```sh
jar cf MyApp.jar MyClass.class Service1.class Service2.class ...

java -jar MyApp.jar
```

### Writing Java docs

```sh
# Create documentation that has a nice html format
javadoc -d doc MyClass.java
```

### Java Build Tools

- Maven
- Gradle
- Ant

Ant, for example, uses an XML configuration file to compile, test, and document with the `ant` cmd

## NodeJS

NPM Commands

```sh
npm -v
npm search file
npm install file
# Check the search path of node (i.e. local, global, etc.)
node -e "console.log(module.paths)"
#=> ['/app/node_modules', '/node_modules']
```

Two types modules
1. Built-in
  - Installed when Node is
  - `/usr/lib/node_modules/npm/node_modules`
  - Examples:
    - fs
    - http
    - os
    - events
    - tls
    - url
2. External
  - `/usr/lib/node_modules`
  - Examples:
    - express
    - react
    - debug
    - async
    - lodash
