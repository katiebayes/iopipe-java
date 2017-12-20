# IOpipe Telemetry Agent for Java

 * <http://www.iopipe.com/>
 * Licensed under the Apache 2.0 License.

This project provides the capability of using the IOPipe service for AWS
lambda services.

This project uses OSHI <https://github.com/oshi/oshi> (which is under the
EPL 1.0 license) to obtain information about the native system.

# Project

## Requirements

This project requires Maven and at least Java 7.

## Building

Building requires Maven and a Java 7 Virtual Machine.

 * `mvn compile`         -- Compile the project.
 * `mvn package`         -- Compile JAR package.
 * `mvn test`            -- Run tests.
 * `mvn clean`           -- Clean build.
 * `mvn site`            -- Generate Maven informational site.
 * `mvn javadoc:javadoc` -- Generate JavaDoc

# System Properties And Environment Variables.

These are used to configure IOPipe from the outside environment.

For compatibility with other IOPipe clients the environment variables are
supported. System properties take precedence.

 * `com.iopipe.debug` or `IOPIPE_DEBUG`
   * If this is set to `true` then
   * If this is not set then it defaults to `false`.
 * `com.iopipe.enabled` or `IOPIPE_ENABLED`
   * If this is set and if the value is `true` (ignoring case) then the library
     will be enabled.
   * If this is set to `false`.
   * If this is not set then internally it is treated as being `true`.
 * `com.iopipe.installmethod` or `IOPIPE_INSTALL_METHOD`
 * `com.iopipe.timeoutwindow` or `IOPIPE_TIMEOUT_WINDOW`
   * This time is subtracted from the duration that a lambda may operate on
     the service, if 
   * If this is zero then the window is disabled.
   * If this is not set then it defaults to `150`.
 * `com.iopipe.token`, `IOPIPE_TOKEN`, or `IOPIPE_CLIENTID`
   * This represents the token of the IOPipe collector which is to obtain
     statistics.
   * This is the default token which will be used if no token was specified in
     the client.
   * If you need help looking for your token you can visit:
     [Find your project token](https://dashboard.iopipe.com/install).

# Integration Into Your Maven Project With Amazon AWS Lambdas

***TO BE WRITTEN COMPLETELY***

The instructions here for setting up your Maven project are similar to the ones
listed on the Amazon site:
<https://docs.aws.amazon.com/lambda/latest/dg/java-create-jar-pkg-maven-no-ide.html>.
There are however differences since your lambda will need to be wrapped
accordingly for it to function and record any statistics.

In your `pom.xml` have the following

```
<dependency>
  <groupId>com.iopipe</groupId>
  <artifactId>iopipe</artifactId>
  <version>1.0-SNAPSHOT</version>
</dependency>

<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-shade-plugin</artifactId>
      <version>2.3</version>
      <configuration>
        <createDependencyReducedPom>false</createDependencyReducedPom>
      </configuration>
      <executions>
        <execution>
          <phase>package</phase>
          <goals>
            <goal>shade</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

If you wish to strip all debugging information in the JAR file you can run
the command:

`pack200 -r -G file.jar`

Note that stack traces will not be as meaningful and will not provide locations
as to where exceptions were thrown.

***TO BE WRITTEN COMPLETELY***

