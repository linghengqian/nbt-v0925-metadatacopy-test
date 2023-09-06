## nbt-v0926-metadatacopy-test

- For https://github.com/apache/shardingsphere/issues/21347
  and https://github.com/baomidou/dynamic-datasource/issues/565 .

- Execute the following command under the new Ubuntu 22.04.3 LTS instance. `./mvnw clean test` is only used to verify 
that unit tests are available.

```bash
 sudo apt install unzip zip curl sed -y
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install java 17.0.8-graalce
sdk use java 17.0.8-graalce
sudo apt-get install build-essential libz-dev zlib1g-dev -y

git clone git@github.com:linghengqian/nbt-v0926-metadatacopy-test.git
cd ./dynamic-datasource/
./mvnw clean test
./mvnw -PgenerateMetadata -DskipNativeTests -T1C -B -e clean test native:metadata-copy
```

- You will find that no files are output. And an exception is thrown during the `metadataCopy` phase.

```bash
$ ./mvnw -PgenerateMetadata -DskipNativeTests -T1C -B -e clean test native:metadata-copy
[INFO] Error stacktraces are turned on.
[INFO] Scanning for projects...
[INFO] Found GraalVM installation from JAVA_HOME variable.
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Build Order:
[INFO] 
[INFO] nbt-v0926-metadatacopy-test                                        [pom]
[INFO] curator-client                                                     [jar]
[INFO] curator-framework                                                  [jar]
[INFO] 
[INFO] Using the MultiThreadedBuilder implementation with a thread count of 6
[INFO] 
[INFO] ---------------< com.lingh:nbt-v0926-metadatacopy-test >----------------
[INFO] Building nbt-v0926-metadatacopy-test 1.0-SNAPSHOT                  [1/3]
[INFO]   from pom.xml
[INFO] --------------------------------[ pom ]---------------------------------
[WARNING] *****************************************************************
[WARNING] * Your build is requesting parallel execution, but this         *
[WARNING] * project contains the following plugin(s) that have goals not  *
[WARNING] * marked as thread-safe to support parallel execution.          *
[WARNING] * While this /may/ work fine, please look for plugin updates    *
[WARNING] * and/or request plugins be made thread-safe.                   *
[WARNING] * If reporting an issue, report it against the plugin in        *
[WARNING] * question, not against Apache Maven.                           *
[WARNING] *****************************************************************
[WARNING] The following plugins are not marked as thread-safe in nbt-v0926-metadatacopy-test:
[WARNING]   org.graalvm.buildtools:native-maven-plugin:0.9.25
[WARNING] 
[WARNING] Enable debug to see precisely which goals are not marked as thread-safe.
[WARNING] *****************************************************************
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ nbt-v0926-metadatacopy-test ---
[INFO] 
[INFO] --- native-maven-plugin:0.9.25:merge-agent-files (test-native) @ nbt-v0926-metadatacopy-test ---
[INFO] 
[INFO] --- native-maven-plugin:0.9.25:test (test-native) @ nbt-v0926-metadatacopy-test ---
[INFO] Skipping native-image tests (parameter 'skipTests' or 'skipNativeTests' is true).
[INFO] 
[INFO] --- native-maven-plugin:0.9.25:metadata-copy (default-cli) @ nbt-v0926-metadatacopy-test ---
[WARNING] Destination directory /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/src/test/resources/META-INF/native-image/com.lingh/nbt-v0926-metadatacopy-test doesn't exist.
[WARNING] Creating directory at: /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/src/test/resources/META-INF/native-image/com.lingh/nbt-v0926-metadatacopy-test
[INFO] Found GraalVM installation from JAVA_HOME variable.
[WARNING] Cannot find source directory /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/target/native/agent-output/test for metadata copy. Please check if you configured agent properly and it generates all necessary directories. If you want to skipp copy from some source, please configure metadataCopy with disable stage you want to skipp.
[INFO] Metadata copy process finished.
[INFO] 
[INFO] ----------------------< com.lingh:curator-client >----------------------
[INFO] 
[INFO] Building curator-client 1.0-SNAPSHOT                               [2/3]
[INFO] --------------------< com.lingh:curator-framework >---------------------
[INFO]   from curator-client/pom.xml
[INFO] Building curator-framework 1.0-SNAPSHOT                            [3/3]
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]   from curator-framework/pom.xml
[INFO] --------------------------------[ jar ]---------------------------------
[WARNING] *****************************************************************
[WARNING] * Your build is requesting parallel execution, but this         *
[WARNING] *****************************************************************
[WARNING] * project contains the following plugin(s) that have goals not  *
[WARNING] * Your build is requesting parallel execution, but this         *
[WARNING] * project contains the following plugin(s) that have goals not  *
[WARNING] * marked as thread-safe to support parallel execution.          *
[WARNING] * marked as thread-safe to support parallel execution.          *
[WARNING] * While this /may/ work fine, please look for plugin updates    *
[WARNING] * While this /may/ work fine, please look for plugin updates    *
[WARNING] * and/or request plugins be made thread-safe.                   *
[WARNING] * and/or request plugins be made thread-safe.                   *
[WARNING] * If reporting an issue, report it against the plugin in        *
[WARNING] * question, not against Apache Maven.                           *
[WARNING] *****************************************************************
[WARNING] The following plugins are not marked as thread-safe in curator-client:
[WARNING]   org.graalvm.buildtools:native-maven-plugin:0.9.25
[WARNING] 
[WARNING] Enable debug to see precisely which goals are not marked as thread-safe.
[WARNING] *****************************************************************
[WARNING] * If reporting an issue, report it against the plugin in        *
[WARNING] * question, not against Apache Maven.                           *
[WARNING] *****************************************************************
[WARNING] The following plugins are not marked as thread-safe in curator-framework:
[WARNING]   org.graalvm.buildtools:native-maven-plugin:0.9.25
[WARNING] 
[WARNING] Enable debug to see precisely which goals are not marked as thread-safe.
[WARNING] *****************************************************************
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ curator-framework ---
[INFO] 
[INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ curator-client ---
[INFO] Deleting /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/curator-framework/target
[INFO] Deleting /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/curator-client/target
[INFO] 
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ curator-client ---
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ curator-framework ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/curator-client/src/main/resources
[INFO] skip non existing resourceDirectory /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/curator-framework/src/main/resources
[INFO] 
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ curator-framework ---
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ curator-client ---
[INFO] No sources to compile
[INFO] No sources to compile
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ curator-framework ---
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ curator-client ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 0 resource
[INFO] Copying 0 resource
[INFO] 
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ curator-framework ---
[INFO] --- maven-compiler-plugin:3.1:testCompile (default-testCompile) @ curator-client ---
[INFO] Changes detected - recompiling the module!
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/curator-framework/target/test-classes
[INFO] Compiling 1 source file to /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/curator-client/target/test-classes
[INFO] 
[INFO] --- maven-surefire-plugin:3.1.2:test (default-test) @ curator-client ---
[INFO] 
[INFO] --- maven-surefire-plugin:3.1.2:test (default-test) @ curator-framework ---
[INFO] Surefire report directory: /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/curator-framework/target/surefire-reports
[INFO] Surefire report directory: /home/linghengqian/TwinklingLiftWorks/git/public/nbt-v0926-metadatacopy-test/curator-client/target/surefire-reports
[INFO] Using auto detected provider org.apache.maven.surefire.junitplatform.JUnitPlatformProvider
[INFO] Using auto detected provider org.apache.maven.surefire.junitplatform.JUnitPlatformProvider
[INFO] 
[INFO] -------------------------------------------------------
[INFO] 
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.lingh.CuratorFrameworkTest
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
[INFO] Running com.lingh.CuratorClientTest
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
SLF4J: Failed to load class "org.slf4j.impl.StaticMDCBinder".
SLF4J: Defaulting to no-operation MDCAdapter implementation.
SLF4J: See http://www.slf4j.org/codes.html#no_static_mdc_binder for further details.
SLF4J: Failed to load class "org.slf4j.impl.StaticMDCBinder".
SLF4J: Defaulting to no-operation MDCAdapter implementation.
SLF4J: See http://www.slf4j.org/codes.html#no_static_mdc_binder for further details.
/testFirst/path - CREATE
/testSecond/path - SET_DATA
/testThird/testSagittarius/path - DELETE
[INFO] Tests run: 3, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 1.868 s -- in com.lingh.CuratorFrameworkTest
[INFO] 
[INFO] Results:
[INFO] 
[INFO] Tests run: 3, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] 
[INFO] --- native-maven-plugin:0.9.25:merge-agent-files (test-native) @ curator-framework ---
[INFO] 
[INFO] --- native-maven-plugin:0.9.25:test (test-native) @ curator-framework ---
[INFO] Skipping native-image tests (parameter 'skipTests' or 'skipNativeTests' is true).
[INFO] 
[INFO] --- native-maven-plugin:0.9.25:metadata-copy (default-cli) @ curator-framework ---
[INFO] Copying files from: test
[ERROR] Metadata copy process failed with code: 1
[INFO] Tests run: 7, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 2.159 s -- in com.lingh.CuratorClientTest
[INFO] 
[INFO] Results:
[INFO] 
[INFO] Tests run: 7, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] 
[INFO] --- native-maven-plugin:0.9.25:merge-agent-files (test-native) @ curator-client ---
[INFO] 
[INFO] --- native-maven-plugin:0.9.25:test (test-native) @ curator-client ---
[INFO] Skipping native-image tests (parameter 'skipTests' or 'skipNativeTests' is true).
[INFO] 
[INFO] --- native-maven-plugin:0.9.25:metadata-copy (default-cli) @ curator-client ---
[INFO] Copying files from: test
[ERROR] Metadata copy process failed with code: 1
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary for nbt-v0926-metadatacopy-test 1.0-SNAPSHOT:
[INFO] 
[INFO] nbt-v0926-metadatacopy-test ........................ SUCCESS [  0.406 s]
[INFO] curator-client ..................................... FAILURE [  6.095 s]
[INFO] curator-framework .................................. FAILURE [  5.690 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  6.873 s (Wall Clock)
[INFO] Finished at: 2023-09-07T05:32:46+08:00
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal org.graalvm.buildtools:native-maven-plugin:0.9.25:metadata-copy (default-cli) on project curator-framework: Metadata copy process failed. -> [Help 1]
org.apache.maven.lifecycle.LifecycleExecutionException: Failed to execute goal org.graalvm.buildtools:native-maven-plugin:0.9.25:metadata-copy (default-cli) on project curator-framework: Metadata copy process failed.
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute2 (MojoExecutor.java:375)
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute (MojoExecutor.java:351)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:215)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:171)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:163)
    at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject (LifecycleModuleBuilder.java:117)
    at org.apache.maven.lifecycle.internal.builder.multithreaded.MultiThreadedBuilder$1.call (MultiThreadedBuilder.java:210)
    at org.apache.maven.lifecycle.internal.builder.multithreaded.MultiThreadedBuilder$1.call (MultiThreadedBuilder.java:195)
    at java.util.concurrent.FutureTask.run (FutureTask.java:264)
    at java.util.concurrent.Executors$RunnableAdapter.call (Executors.java:539)
    at java.util.concurrent.FutureTask.run (FutureTask.java:264)
    at java.util.concurrent.ThreadPoolExecutor.runWorker (ThreadPoolExecutor.java:1136)
    at java.util.concurrent.ThreadPoolExecutor$Worker.run (ThreadPoolExecutor.java:635)
    at java.lang.Thread.run (Thread.java:833)
Caused by: org.apache.maven.plugin.MojoExecutionException: Metadata copy process failed.
    at org.graalvm.buildtools.maven.MetadataCopyMojo.executeCopy (MetadataCopyMojo.java:163)
    at org.graalvm.buildtools.maven.MetadataCopyMojo.execute (MetadataCopyMojo.java:115)
    at org.apache.maven.plugin.DefaultBuildPluginManager.executeMojo (DefaultBuildPluginManager.java:137)
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute2 (MojoExecutor.java:370)
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute (MojoExecutor.java:351)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:215)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:171)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:163)
    at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject (LifecycleModuleBuilder.java:117)
    at org.apache.maven.lifecycle.internal.builder.multithreaded.MultiThreadedBuilder$1.call (MultiThreadedBuilder.java:210)
    at org.apache.maven.lifecycle.internal.builder.multithreaded.MultiThreadedBuilder$1.call (MultiThreadedBuilder.java:195)
    at java.util.concurrent.FutureTask.run (FutureTask.java:264)
    at java.util.concurrent.Executors$RunnableAdapter.call (Executors.java:539)
    at java.util.concurrent.FutureTask.run (FutureTask.java:264)
    at java.util.concurrent.ThreadPoolExecutor.runWorker (ThreadPoolExecutor.java:1136)
    at java.util.concurrent.ThreadPoolExecutor$Worker.run (ThreadPoolExecutor.java:635)
    at java.lang.Thread.run (Thread.java:833)
[ERROR] Failed to execute goal org.graalvm.buildtools:native-maven-plugin:0.9.25:metadata-copy (default-cli) on project curator-client: Metadata copy process failed. -> [Help 1]
org.apache.maven.lifecycle.LifecycleExecutionException: Failed to execute goal org.graalvm.buildtools:native-maven-plugin:0.9.25:metadata-copy (default-cli) on project curator-client: Metadata copy process failed.
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute2 (MojoExecutor.java:375)
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute (MojoExecutor.java:351)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:215)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:171)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:163)
    at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject (LifecycleModuleBuilder.java:117)
    at org.apache.maven.lifecycle.internal.builder.multithreaded.MultiThreadedBuilder$1.call (MultiThreadedBuilder.java:210)
    at org.apache.maven.lifecycle.internal.builder.multithreaded.MultiThreadedBuilder$1.call (MultiThreadedBuilder.java:195)
    at java.util.concurrent.FutureTask.run (FutureTask.java:264)
    at java.util.concurrent.Executors$RunnableAdapter.call (Executors.java:539)
    at java.util.concurrent.FutureTask.run (FutureTask.java:264)
    at java.util.concurrent.ThreadPoolExecutor.runWorker (ThreadPoolExecutor.java:1136)
    at java.util.concurrent.ThreadPoolExecutor$Worker.run (ThreadPoolExecutor.java:635)
    at java.lang.Thread.run (Thread.java:833)
Caused by: org.apache.maven.plugin.MojoExecutionException: Metadata copy process failed.
    at org.graalvm.buildtools.maven.MetadataCopyMojo.executeCopy (MetadataCopyMojo.java:163)
    at org.graalvm.buildtools.maven.MetadataCopyMojo.execute (MetadataCopyMojo.java:115)
    at org.apache.maven.plugin.DefaultBuildPluginManager.executeMojo (DefaultBuildPluginManager.java:137)
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute2 (MojoExecutor.java:370)
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute (MojoExecutor.java:351)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:215)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:171)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:163)
    at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject (LifecycleModuleBuilder.java:117)
    at org.apache.maven.lifecycle.internal.builder.multithreaded.MultiThreadedBuilder$1.call (MultiThreadedBuilder.java:210)
    at org.apache.maven.lifecycle.internal.builder.multithreaded.MultiThreadedBuilder$1.call (MultiThreadedBuilder.java:195)
    at java.util.concurrent.FutureTask.run (FutureTask.java:264)
    at java.util.concurrent.Executors$RunnableAdapter.call (Executors.java:539)
    at java.util.concurrent.FutureTask.run (FutureTask.java:264)
    at java.util.concurrent.ThreadPoolExecutor.runWorker (ThreadPoolExecutor.java:1136)
    at java.util.concurrent.ThreadPoolExecutor$Worker.run (ThreadPoolExecutor.java:635)
    at java.lang.Thread.run (Thread.java:833)
[ERROR] 
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR] 
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoExecutionException
[ERROR] 
[ERROR] After correcting the problems, you can resume the build with the command
[ERROR]   mvn <args> -rf :curator-framework
```