[//]: # (title: Gradle Application plugin)

<tldr>
<p>
<control>Sample project</control>: <a href="https://github.com/ktorio/ktor-documentation/tree/%ktor_version%/codeSnippets/snippets/engine-main">engine-main</a>
</p>
</tldr>

The Gradle [Application plugin](https://docs.gradle.org/current/userguide/application_plugin.html) provides the ability to package applications, including code dependencies and generated start scripts. In this topic, we'll show you how to package and run a Ktor application.


## Apply the Application plugin and configure the main class {id="apply-plugin"}
To package an application, you need to apply the Application plugin first:
1. Open the `build.gradle(.kts)` file of your project.
2. Make sure that the file contains the following code:

   <tabs group="languages">
   <tab title="Gradle (Kotlin)" group-key="kotlin">

   ```kotlin
   ```
   {src="snippets/engine-main/build.gradle.kts" include-lines="5-6,8-12"}

   </tab>
   <tab title="Gradle (Groovy)" group-key="groovy">

   ```groovy
   plugins {
       id 'application'
   }
   
   application {
       mainClass = 'io.ktor.server.netty.EngineMain'
   }
   ```

   </tab>
   </tabs>
   
   * The Application plugin is applied inside the `plugins` block.
   * The `mainClass` property is used to configure the main class of the application. Note that the application main class depends on the way used to [create a server](create_server.topic).
     In the example above, the main class depends on the used engine and looks as follows: `io.ktor.server.netty.EngineMain`.


## Package the application {id="package"}
The Application plugin provides various ways for packaging the application, for example, the `installDist` task installs the application with all runtime dependencies and start scripts. To create full distribution archives, you can use the `distZip` and `distTar` tasks.

In this topic, we'll use `installDist`:
1. Open a terminal.
2. Run the `installDist` task in one of the following ways depending on your operating system:
   
   <tabs group="os">
   <tab title="Linux/macOS" group-key="unix">
   <code-block>./gradlew installDist</code-block>
   </tab>
   <tab title="Windows" group-key="windows">
   <code-block>gradlew.bat installDist</code-block>
   </tab>
   </tabs>
   
   Gradle will create an image of the application in the `build/install/<project_name>` folder. 


## Run the application {id="run"}
To run the [packaged application](#package):
1. Go to the `build/install/<project_name>/bin` folder in a terminal.
2. Depending on your operating system, run the `<project_name>` or `<project_name>.bat` executable, for example:

   <snippet id="run_executable">
   <tabs group="os">
   <tab title="Linux/macOS" group-key="unix">
   <code-block>./ktor-sample</code-block>
   </tab>
   <tab title="Windows" group-key="windows">
   <code-block>ktor-sample.bat</code-block>
   </tab>
   </tabs>
   </snippet>
   
3. Wait until the following message is shown:
   ```Bash
   [main] INFO  Application - Responding at http://0.0.0.0:8080
   ```
   Open the link in a browser to see a running application:

   <img src="ktor_idea_new_project_browser.png" alt="Ktor app in a browser" width="430"/>