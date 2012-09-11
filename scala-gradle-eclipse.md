[title:Scala project using Gradle and Eclipse]: /
[tags: {scala, eclipse, gradle, scalatest}]: /
[category:programming]: /
[order:20]: /
[serve:false]: /
# Scala development with Eclipse, Gradle and Scalatest   ###

## Configuration  ###
The first step is to install Eclipse. The Scala-IDE doesn't support 4.2 yet, so use 3.7.2.

Install the Gradle plugin as well as the Groovy plugin. This provides some gradle DSL support in build scripts (once you enable the DSL on a project in Eclipse).

Use the Scala-IDE ecosystem update site. I used the dev-master-2.9 version. This includes both Scala-IDE and ScalaTest plugins. By using the plugin, can write Scalatest files, and don't need to use the JUnit runner.

For Gradle build, use the scala plugin, and also modify the test task to recognize scalatest tests. See [Getting Into Scala and Gradle](http://martingladdish.co.uk/blog/2010/10/31/getting-into-scala-and-gradle/) for good instructions.

Suggest using this code rather than code used on previous link

	test << {
    		ant.taskdef(name: 'scalatest', classname: 'org.scalatest.tools.ScalaTestAntTask', classpath: classpath.asPath)
    		ant.scalatest(runpath: testClassesDir, haltonfailure: 'true', fork: 'false') {
        		reporter(type: 'stdout')
    	}
	}

Currently, not the greatest. Added test with pending and with failure. Works fine within Eclipse, as shows test that's in error.

When run via Gradle build, can run normally, and Gradle will report that tests failed. Unfortunately, by default, it doesn't show any details.

To show details, one must call Gradle with the --info option. Then Scalatest will show all of its logging information. I haven't found a way around this yet, but with any luck, I will.