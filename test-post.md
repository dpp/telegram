[title:Scala project using Gradle and Eclipse]:
[date:2012-09-01]:
[tags: {scala, eclipse, gradle, scalatest}]:
[category:programming]:
[post:true]:

**This is a work in progress. Quick notes now, and will tidy up later**

## Configuration ##
The first step is to install Eclipse. The Scala-IDE doesn't support 4.2 yet, so use 3.7.2.

Install the Gradle plugin as well as the Groovy plugin. This provides some gradle DSL support in build scripts (once you enable the DSL on a project in Eclipse).

Also add the scala-ide ecosystem update site. This will allow for install of both Scala-IDE and Scalatest. 

By using the IDE plugin for Scalatest, don't need JUnit runner. 

For Gradle build, use the scala plugin, and also modify the test task to recognize scalatest tests. See [Getting Into Scala and Gradle](http://martingladdish.co.uk/blog/2010/10/31/getting-into-scala-and-gradle/) for good instructions.

Suggest using this code rather than code used on previous link

	test << {
    		ant.taskdef(name: 'scalatest', classname: 'org.scalatest.tools.ScalaTestAntTask', classpath: classpath.asPath)
    		ant.scalatest(runpath: testClassesDir, haltonfailure: 'true', fork: 'false') {
        		reporter(type: 'stdout')
    	}
	}

Currently, not the greatest. Added test with pending and with failure. Works fine within Eclipse, as shows test that's in error.

When run via Gradle build, build merely fails stating that ScalaTest didn't complete successfully. Need to dig into having this be much better. Is this how it works with Ant (as that's what we're using in the Gradle build too).
