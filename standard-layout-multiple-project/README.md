In this example we have 3 projects. Root, project1, and project2. Project2 depends on project1, the output from project1 is put into the testCompile configuration for project2. The following is the output listing all the dependencies for all three projects.

    ~/w/g/standard-layout-multiple-project git:master ❯❯❯ gradle dependencies :project1:dependencies :project2:dependencies 
    :dependencies

    ------------------------------------------------------------
    Root project
    ------------------------------------------------------------

    No configurations
    :project1:dependencies

    ------------------------------------------------------------
    Project :project1
    ------------------------------------------------------------

    archives - Configuration for archive artifacts.
    No dependencies

    compile - Compile classpath for source set 'main'.
    \--- junit:junit:4.11
         \--- org.hamcrest:hamcrest-core:1.3

    default - Configuration for default artifacts.
    \--- junit:junit:4.11
         \--- org.hamcrest:hamcrest-core:1.3

    runtime - Runtime classpath for source set 'main'.
    \--- junit:junit:4.11
         \--- org.hamcrest:hamcrest-core:1.3

    testCompile - Compile classpath for source set 'test'.
    +--- junit:junit:4.11
    |    \--- org.hamcrest:hamcrest-core:1.3
    \--- org.apache.commons:commons-lang3:3.3.2

    testRuntime - Runtime classpath for source set 'test'.
    +--- junit:junit:4.11
    |    \--- org.hamcrest:hamcrest-core:1.3
    \--- org.apache.commons:commons-lang3:3.3.2
    :project2:dependencies

    ------------------------------------------------------------
    Project :project2
    ------------------------------------------------------------

    archives - Configuration for archive artifacts.
    No dependencies

    compile - Compile classpath for source set 'main'.
    \--- com.mchange:c3p0:0.9.5-pre8
         \--- com.mchange:mchange-commons-java:0.2.7

    default - Configuration for default artifacts.
    \--- com.mchange:c3p0:0.9.5-pre8
         \--- com.mchange:mchange-commons-java:0.2.7

    runtime - Runtime classpath for source set 'main'.
    \--- com.mchange:c3p0:0.9.5-pre8
         \--- com.mchange:mchange-commons-java:0.2.7

    testCompile - Compile classpath for source set 'test'.
    +--- com.mchange:c3p0:0.9.5-pre8
    |    \--- com.mchange:mchange-commons-java:0.2.7
    \--- project :project1
         \--- junit:junit:4.11
              \--- org.hamcrest:hamcrest-core:1.3

    testRuntime - Runtime classpath for source set 'test'.
    +--- com.mchange:c3p0:0.9.5-pre8
    |    \--- com.mchange:mchange-commons-java:0.2.7
    \--- project :project1
         \--- junit:junit:4.11
          \--- org.hamcrest:hamcrest-core:1.3

    BUILD SUCCESSFUL

    Total time: 0.852 secs

 
As you can see project1 and project two have different dependencies for the compile configuration. Project1 has junit in it, and project2 has c3p0. Configurations can have dependencies between themselves. For example runtime includes the compile configuration. By this property, you can see that the testCompile for project2 has the compile configurations for both project1 and project2. This is because project2 depends on project1 at the testCompile configuration.

![gradle documenation](http://www.gradle.org/docs/current/userguide/img/javaPluginConfigurations.png)

You can also see that project2's testRuntime doesn't contain 'org.apache.commons:commons-lang3:3.3.2', because the runtime output is what gets included when you depend on projects
