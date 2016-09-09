---
layout: post
title:  "Overriding user defined configuration of Log4j2, programatically with Custom 'configurationFactory'"
date:   2016-09-09 23:30:01 +0530
categories: blogs java logging log4j2
image: /assets/images/log4j2.png
linkText: Read More
tags: [Java, Logging, Log4j2, Log4j]
comments: true
disqus_identifier: 3
---

There are many ways to configure log4j2 via xml file or a properties file etc, but this becomes a problem when your application is based on microservices architecture. Every other developer writes its own configuration file with different pattern layouts and appenders config leading to a mess and to add to this think of a situation when you are aggregating logs all those applications to a single place. All those different appender layouts and formats lead to unreadable logs that makes little to no sense.

ConfigurationFactory lets you control the above problems, think of it as including a single dependecy in all the microservices/applications that you have built and it configures the logging system for you, and whenever you like just releasing a new version of the same to make changes.

Now, what is this ConfigurationFactory class :- ConfigurationFactory is a factory for parsed Configuration that is read from the config files (log4j2.xml etc). It can be provided in one of the three ways :-

 1. Providing log4j.configurationFactory command line argument to fully qualified class name.
 2. Using ConfigurationFactory.setConfigurationFactory(ConfigurationFactory factory) method to set a class before any call is made to a log4j.
 3. Providing a ConfigurationFactory implementation in the classpath and configured as a plugin in the ConfigurationFactory category. Moreover an @Order annotation can be used to provide priorrity if multiple instances of ConfigurationFactory are present in the classpath.

To better understand, lets have a look at the below code snippet

<script src="https://gist.github.com/shivamkh90/af75d3c5f719c92a2efeddfad827734c.js"></script>

By overriding the getConfiguration method, you can provide your custom configuration from the factory class and by overriding getSupportedTypes we are effectively trying to say that this ConfigurationFaactory implementation is applicable for all types of configuration provided.

'createConfiguration' method uses a ConfigurationBuilder object to provide configuration.

@Order annotation comes into play when there are multiple implementations of ConfigurationFactory present in the classpath and the decision as to which will be chosen to get configuration depends on the priority provided to @Order annotation, higher the number lower is its priority. Also if a configuration factory's getConfiguration method returns null then the next lower priority configurationFactory will be chosen to retrieve the same until there is no configurationfactory object is left in the chain, then in that case the default ConfigurationFactory object will be chosen to retrieve the conf.

Now what if you want to use the properties file or xml file formats defined by log4j2  to initialize your custom configuration, you may do this by extending, one of the several implementations of ConfigurationFactory for different formats such as PropertiesConfigurationFactory for reading from a properties file and just call its getConfiguration method from your child class with the custom property file that you have shipped with your dependency. Example follows :-

<script src="https://gist.github.com/shivamkh90/e7a2ed448405bd977e8bb0adc8d03f48.js"></script>

Moreover, you can read this properties file from anywhere it can be a url of a centralized property file for all your application.

More examples and complete reference can be found at [Apache Log4j2](https://logging.apache.org/log4j/2.x/manual/customconfig.html).



Thanks for reading, see you next time.
