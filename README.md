[![GitHub Actions](https://github.com/seleniumhq/seleniumhq.github.io/workflows/Publish%20Selenium%20Site/badge.svg)](https://github.com/SeleniumHQ/seleniumhq.github.io/actions?query=workflow%3A%22Publish+Selenium+Site%22)

<a href="https://selenium.dev"><img src="https://selenium.dev/images/selenium_logo_square_green.png" width="200" alt="Selenium"/></a>

# Selenium Site and Documentation

This is the repository used to build and publish the official Selenium [website](https://selenium.dev).

## Quick start

We use [Hugo](https://gohugo.io/) and the [Docsy theme](https://www.docsy.dev/)
to build and render the site. You will need the **extended**
Sass/SCSS version of the Hugo binary to work on this site. We recommend
to use Hugo 0.125.4

Steps needed to have this working locally and work on it:

- Follow the [Install Hugo](https://www.docsy.dev/docs/get-started/other-options/#install-hugo) instructions from Docsy
- [Install go](https://go.dev/doc/install)
- Clone this repository
- Run `cd website_and_docs`
- Run `hugo server`

A full contribution guideline can be seen at [contributing](https://selenium.dev/documentation/about/contributing/)

## How to get involved?

Please check all the information available at https://selenium.dev/getinvolved/

### Do not want to clone the repository to contribute? Use GitPod.

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/SeleniumHQ/seleniumhq.github.io)


## For Selenium Site and Documentation maintainers

### How does the site and docs get build?

GitHub actions runs for every commit on each PR and protected branch. The regular CI execution will
build the site with Hugo to verify that the commit works. The description of these steps can be seen
at the actions configuration file, [one for testing a PR](./.github/workflows/test.yml), and 
[one for deploying the site](./.github/workflows/deploy.yml)

### How are the site and docs deployed?

After each CI execution that happens in the `trunk` branch, the script [build-site.sh](./build-site.sh) 
is executed for deployment. This script checks for the string `[deploy site]` in the commit message.

If the commit message contains that string, and the commit is in `trunk`, a 
[GitHub action](./.github/workflows/deploy.yml) is triggered to build and deploy the site. 
The site and docs will be built, and the changes will be committed to the branch `publish` 
by the user [Selenium-CI](https://github.com/selenium-ci/).

*What is important to take into account is that the source files for the site are in the `trunk`
branch, and the files that get deployed are pushed to the `publish` branch.*

The site is deployed using GitHub pages, and the configuration for this can be seen at the
repo [settings](https://github.com/SeleniumHQ/seleniumhq.github.io/settings) (if you are a maintainer
you should be able to access the link).

The selenium.
domain is managed at https://www.gandi.net/en, if you need access to it, reach out to
any of the [PLC](https://www.selenium.dev/project/structure/#plc) or [TLC](https://www.selenium.dev/project/structure/#tlc)
members, who can help you with that.

If for any reason, you need to setup the domain redirection again,
we followed this [guide](http://spector.io/how-to-set-up-github-pages-with-a-custom-domain-on-gandi/),
but any tutorial/guide showing how to redirect a domain to GitHub pages should do.   


Maven plugins examples
=============================


Maven Plugins:
==============

Here are examples of different useful Maven plugins, showing their typical usage in a `pom.xml` file:

---

### 1. **Maven Compiler Plugin**
Compiles Java source code.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-compiler-plugin</artifactId>
  <version>3.11.0</version>
  <configuration>
    <source>17</source>
    <target>17</target>
  </configuration>
</plugin>
```
==>

<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>maven-compiler-plugin-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <build>
        <plugins>
            <!-- Maven Compiler Plugin Example -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.11.0</version>
                <configuration>
                    <source>17</source> <!-- Java source version -->
                    <target>17</target> <!-- Java target version -->
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>

How to use:

Place the above in your pom.xml.
Change <source> and <target> to your desired Java version (e.g., 8, 11, 17).
Run mvn compile in your project directory.
Maven will use the specified Java version for compilation.


---

### 2. **Maven Surefire Plugin**
Runs unit tests.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-surefire-plugin</artifactId>
  <version>3.1.2</version>
</plugin>
```
==>

<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>surefire-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <build>
        <plugins>
            <!-- Maven Surefire Plugin: runs unit tests -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.1.2</version>
                <configuration>
                    <includes>
                        <include>**/*Test.java</include>
                    </includes>
                    <!-- You can configure other options here, e.g., system properties, parallel execution, etc. -->
                </configuration>
            </plugin>
        </plugins>
    </build>

    <dependencies>
        <!-- Example: JUnit for testing -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.10.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>

How to use:

Add this plugin section to your pom.xml.
Place your test classes (e.g., ExampleTest.java) in src/test/java.
Run your tests via Maven

	mvn test

Surefire will automatically execute your unit tests and provide a summary in the console and reports in target/surefire-reports/.
Tip:
You can further customize Surefire with options like parallel execution, test includes/excludes, system properties, listeners, etc.
---

### 3. **Maven Failsafe Plugin**
Runs integration tests.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-failsafe-plugin</artifactId>
  <version>3.1.2</version>
  <executions>
    <execution>
      <goals>
        <goal>integration-test</goal>
        <goal>verify</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```
==>

<project>
  ...
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-failsafe-plugin</artifactId>
        <version>3.1.2</version>
        <executions>
          <execution>
            <goals>
              <goal>integration-test</goal>
              <goal>verify</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <!-- Optional: specify patterns for integration test classes -->
          <includes>
            <include>**/IT*.java</include>
            <include>**/*IT.java</include>
          </includes>
        </configuration>
      </plugin>
    </plugins>
  </build>
  ...
</project>

How to use:

Place your integration test classes in src/test/java and name them like MyServiceIT.java or ITMyService.java.
Run integration tests with

mvn verify


The Failsafe Plugin will execute your integration tests during the integration-test phase and verify results in the verify phase.

Tip:

Use Failsafe for integration tests, and Surefire for unit tests.
Failsafe ensures that a failing integration test does not skip the verify phase, allowing proper reporting.
---

### 4. **Maven Shade Plugin**
Creates an uber/fat JAR with all dependencies.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-shade-plugin</artifactId>
  <version>3.5.0</version>
  <executions>
    <execution>
      <phase>package</phase>
      <goals>
        <goal>shade</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

==> 

<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>shade-demo</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <dependencies>
        <!-- Example dependency -->
        <dependency>
            <groupId>com.google.guava</groupId>
            <artifactId>guava</artifactId>
            <version>33.0.0-jre</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.5.0</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <transformers>
                                <!-- Adds Main-Class to manifest -->
                                <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <mainClass>com.example.Main</mainClass>
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>

Usage:

Add the plugin section above to your pom.xml.
Run mvn package.
Your fat/uber JAR will be created in the target/ directory, containing all dependencies.
You can run it with:
java -jar target/shade-demo-1.0.0.jar
Tip:
Change com.example.Main in <mainClass> to your actual main class.

---

### 5. **Maven Assembly Plugin**
Creates archive files, such as ZIPs or custom JARs.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <version>3.6.0</version>
  <configuration>
    <descriptorRefs>
      <descriptorRef>jar-with-dependencies</descriptorRef>
    </descriptorRefs>
  </configuration>
  <executions>
    <execution>
      <phase>package</phase>
      <goals>
        <goal>single</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```
==>  Maven Assembly Plugin to package your Java project (including all dependencies) into a single JAR file.

<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-assembly-plugin</artifactId>
      <version>3.6.0</version>
      <configuration>
        <archive>
          <manifest>
            <mainClass>com.example.MainClass</mainClass>
          </manifest>
        </archive>
        <descriptorRefs>
          <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
      </configuration>
      <executions>
        <execution>
          <id>make-assembly</id> <!-- this is just an identifier -->
          <phase>package</phase> <!-- bind to the package phase -->
          <goals>
            <goal>single</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>

Step 2: Build the Project

	mvn clean package

After the build, you’ll find a jar file named like yourproject-1.0-SNAPSHOT-jar-with-dependencies.jar in the target directory.
This jar includes your code and all dependencies—ready to run with java -jar.

Tip:
You can also customize the assembly with a descriptor file for ZIP, TAR, or other formats.
For more details, see the official documentation.


---

### 6. **Maven Javadoc Plugin**
Generates Javadoc documentation.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-javadoc-plugin</artifactId>
  <version>3.6.3</version>
</plugin>
```
==>  Maven Javadoc Plugin in your pom.xml to generate Javadoc documentation for your Java project:


<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-javadoc-plugin</artifactId>
      <version>3.6.3</version>
      <executions>
        <execution>
          <id>attach-javadocs</id>
          <goals>
            <goal>jar</goal>
          </goals>
        </execution>
      </executions>
      <configuration>
        <!-- Optional: Encoding, Java version, additional options -->
        <encoding>UTF-8</encoding>
        <source>17</source>
        <show>public</show>
      </configuration>
    </plugin>
  </plugins>
</build>

How to use:

	mvn javadoc:javadoc

This generates Javadoc HTML files in your target/site/apidocs directory.


To create a Javadoc JAR for distribution, run:

	mvn javadoc:jar
This produces a JAR file with your documentation in target/.


Tip:
You can further customize the plugin (for links, suppressing warnings, etc.) using the <configuration> section.
---

### 7. **Maven Clean Plugin**
Removes target directory before building.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-clean-plugin</artifactId>
  <version>3.3.2</version>
</plugin>
```

==>  Maven Clean Plugin is used to remove the target directory and all the files generated by the previous build. This is usually run with the mvn clean command before a build.

<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-clean-plugin</artifactId>
  <version>3.3.2</version>
  <configuration>
    <filesets>
      <fileset>
        <directory>${project.build.directory}</directory>
        <includes>
          <include>*.log</include>
        </includes>
      </fileset>
    </filesets>
  </configuration>
</plugin>

This configuration:

Uses version 3.3.2 of the plugin.
Cleans the target directory (default).
Additionally, removes any .log files in the build directory.

How to Run

From the command line, execute:

mvn clean

This will delete the target directory and any additional files specified in the plugin configuration.


Tip:
You usually don’t need custom configuration unless you want to clean up more than the default build output.
You can also run mvn clean install to clean and then build your project.


---

### 8. **Maven Dependency Plugin**
Manages and analyzes dependencies.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-dependency-plugin</artifactId>
  <version>3.6.1</version>
</plugin>
```
==>  Maven Dependency Plugin provides goals for analyzing, resolving, copying, and managing dependencies. Here’s a basic example of how to use it in your pom.xml, and some common goals you can run.


<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-dependency-plugin</artifactId>
      <version>3.6.1</version>
      <executions>
        <execution>
          <id>copy-dependencies</id>
          <phase>prepare-package</phase>
          <goals>
            <goal>copy-dependencies</goal>
          </goals>
          <configuration>
            <outputDirectory>${project.build.directory}/libs</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>

This example will copy all runtime dependencies to the target/libs folder during the build.

Common Usage from Command Line:
Analyze dependencies:
mvn dependency:analyze

List dependencies:
mvn dependency:list

Copy dependencies:
mvn dependency:copy-dependencies

Get dependency tree:
mvn dependency:tree

Unpack a dependency:
mvn dependency:unpack -Dartifact=groupId:artifactId:version -DoutputDirectory=target/unpacked

Tip:
You can use this plugin to troubleshoot dependency issues, copy JARs for packaging, or analyze unused dependencies in your project.


---

### 9. **Maven Site Plugin**
Generates a project site.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-site-plugin</artifactId>
  <version>4.0.0-M13</version>
</plugin>
```

==>

<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-site-plugin</artifactId>
      <version>4.0.0-M13</version>
      <configuration>
        <!-- Optional: Set the site output directory -->
        <outputDirectory>site-output</outputDirectory>
      </configuration>
    </plugin>
  </plugins>
</build>

How to use:

Add the plugin configuration above to your pom.xml.
Run the following Maven command in your project directory:

mvn site

This will generate a project documentation website (including reports, Javadoc, dependency info, and more) inside the target/site or your configured output directory.

Tip:
You can further customize the site content and appearance using <reporting> section, site descriptors, or adding custom reports.
For example, to include Javadoc and Surefire reports:

<reporting>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-javadoc-plugin</artifactId>
    </plugin>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-report-plugin</artifactId>
    </plugin>
  </plugins>
</reporting>


---

### 10. **Maven Resources Plugin**
Copies and filters resources.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-resources-plugin</artifactId>
  <version>3.3.1</version>
</plugin>
```
==>   give an example how to use Maven Resources Plugin 


<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>resources-plugin-demo</artifactId>
  <version>1.0-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
        <version>3.3.1</version>
        <executions>
          <execution>
            <id>copy-resources</id>
            <phase>process-resources</phase>
            <goals>
              <goal>copy-resources</goal>
            </goals>
            <configuration>
              <outputDirectory>${project.build.directory}/extra-resources</outputDirectory>
              <resources>
                <resource>
                  <directory>src/main/resources-extra</directory>
                  <includes>
                    <include>**/*.txt</include>
                    <include>**/*.properties</include>
                  </includes>
                  <filtering>true</filtering>
                </resource>
              </resources>
            </configuration>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>


How this works:

This example configures the Maven Resources Plugin to copy all .txt and .properties files from src/main/resources-extra to target/extra-resources.
The <filtering>true</filtering> option allows you to use Maven property placeholders (e.g., ${project.version}) in your resource files.
Runs in the process-resources phase.

Basic usage:

By default, Maven copies files from src/main/resources to target/classes without special configuration.
The above example shows how to copy additional resources or customize behavior.

mvn resources:copy-resources


---

**Tip:**  
Most plugins are used in the `<build><plugins></plugins></build>` section in your `pom.xml`.  
You can customize goals, executions, and configurations as needed for your project.


