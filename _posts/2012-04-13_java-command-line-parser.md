[title: Java command line parser]: /
[alias: /2012/04/13/java-command-line-parser/]: /
[date: 2012-04-13]: /

Had a need to write a command line utility for the project I'm on. Was originally using the Apache Commons CLI parser, but it was cumbersome and not that powerful.

Did a bit of searching on StackOverflow, and found <a href="http://jcommander.org/">JCommander</a>. Written by Cedric Beust (author of <a href="testng.org">TestNG</a>). It's a very powerful toolset for dealing with commandlines.

At the simplest, define an arguments object, create fields of the appropriate type, annotate accordingly, and it will parse the results and report errors about type issues etc. If it's successful, you'll have an arguments object pre-populated and ready to use.

More powerful features allow for definition of multiple commands, and corresponding arguments. 

Well worth checking out if you need to parse a command line using Java.


