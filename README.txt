Overview
---------------------------

This project contains an NANT build script that will convert the ZooKeeper server into .NET IL code utilizing IKVM.

Uses
---------------------------

An .NET IL version of ZooKeeper allows for easier integration into systems 
that run on Microsoft .NET 4.0 or Mono with the use of AppDomains. ZooKeeper
can be spawned in a Child AppDomain and management by a service level container. 

It also removes the need to have a Java Virtual Machine (tm) installed. Although 
IKVM is an implementation of a JVM that utilizes OpenJDK for class libraries.

How to build
---------------------------

Note: In order for ZooKeeper to run it requires ZooKeeper 3.4.1 or greater. This includes an enhancement to ZooKeeper to 
      use a new MBeanServer in the event the PlatformMBean cannot be found. Newer versions of IKVM may no longer throw java.lang.Error	  
	  when attempting to get the PlatformMBean server.

From a windows command line that contains nant in the path:

set IKVM_HOME=c:\ikvm
set ZK_HOME=C:\zookeeper
nant

This produces the following files:

    build\Apache.ZooKeeper.exe
		A ready to run executable that will launch a ZooKeeper node given a ZooKeeper configuration file
		as it's first parameter.
	build\Apache.ZooKeeper.dll
		An .NET/Mono Assembly class library that contains all of the ZooKeeper functionality. This assembly can
		be referenced by another .NET project to start/stop nodes.
	build\Apache.ZooKeeper.exe.config
		A .NET/Mono specific configuration file to set common Java System Properties. This is the only 
		way to set equivalant -D system properties with IKVM.
	build\Apache.ZooKeeper.cfg
		A default ZooKeeper configuration file. This contains the same information the Java version uses.
	build\IKVM.* 
		All the required IKVM Assemblies to run ZooKeeper taken from IKVM_HOME
	
	
To-do
---------------------------

* Enhance NAnt build file to utilize Mono to run IKVMC.exe on *nix systems.
* Add a log4net bridge through slf4j and remove log4j dependency.
* Find a way to reduce the IKVM dependencies as it requires almost all the Assemblies to run.
* Reduce the binary size of Apache.ZooKeeper.dll
* Add a .NET Class wrapper for configuring ZooKeeper when utilizing Apache.ZooKeeper.dll
* Add NAnt target to run ZooKeeper's unit tests utilizing IKVM