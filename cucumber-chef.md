[title:Cucumber-Chef Notes]: /
[menu:cucumber-chef]: /
[order:40]:/
# Cucumber-chef Usage ###

## Gotchas and Helpful Advice ###
- if use `create`, the feature is created in the user's home directory.
- when running tests, will look for features in same directory as the .cucumber-chef directory used for configuration
- regardless of the .cucumber-chef directory being used, the log gets written to ~/.cucumber-chef
- if the chef-client can't find something (cookbook/role/recipe), it tends to report a "Net::HTTPServerException: 412 "Precondition Failed"" message. Use the diagnose command to see the chef.log. Generally the chef-client can't find something on the server, and the chef.log will provide details. You will have to scroll up a ways to find out exactly what's missing, but it should be there.
- When running into issues, remember diagnose command. By default, shows chef-stacktrace.out and first line of chef.log. If want more of chef.log file, need to pass -n with number of lines. If don't want chef-stacktrace.out, pass --no-strace. --no-log for no chef.log output.
- Chef Steps: the path is relative to the features location BUT will only find files within the features directory. When running tests, uploads all files in the features directory to the AWS test server. Assumes all directories OTHER THAN support are features, and will validate them. So, cookbooks need to be shimmed into the support directory so features can confirm that they're uploaded correctly.
- uploading databags. If have app/someitem as the contents, want |app|./support/databags/app| as the table entry. This will upload all items within the app directory as databag items.

## Configuration ###
Instructions are at [cucumber-chef instructions](https://github.com/Atalanta/cucumber-chef/wiki). In order to use the test project, ensure you've uploaded the community chef-client cookbook to the generated Chef Server.

### Initialize Cucumber ###
Run `cucumber-chef init`. By default, it creates the cucumber-chef config in your home directory. 

If you leave it here, cucumber-chef will do all runs from your home directory. _This also means you will have to have your features defined here._ 

If you do not want your features defined in your home directory (I recommend having them in your project directory, but ignored by VCS), move or copy the .cucumber-chef folder to the same parent that will contain your features. Cucumber-chef will look in the current directory for a .cucumber-chef directory, and if not found, then look in the ~ directory.

## Setup test bed on AWS ###
Run `cucumber-chef setup`. This takes awhile as it creates an instance on Amazon, and then provisions it with a Chef server and other support files.

Note: Only one chef test bed can exist for an AWS account. So, if want one/developer, will have to ensure each has their own account.

## Create a sample feature ###
Run `cucumber-chef create {project-name}`. This appears to create the feature in your home directory as well. 

This folder can be moved anywhere as long as a .cucumber-chef configuration directory exists in the same parent. 

Again, I would recommend putting the feature under your project directory alongside the .cucumber-chef config directory. Add the feature to your VCS.

## Initialize the test bed Chef Server with mandatory cookbook ###
Get the chef-client recipe installed on the generated chef server. I used berkshelf to download the cookbook, and then used the `cc-knife cookbook upload chef-client`. This assumes your knife.rb file is configured correctly. I have mine defined in ~/.chef and have the cookbooks folder defined as './cookbooks'.

## Execute the sample feature ###
Run the default generated test. This will take quite awhile as both the test project server will need to be provisioned, and the lxc distro cache. Once the lxc distro cache is built, this step will not be required going forwards.

If there are issues running the sample feature, check the notes on the cucumber-chef site for details and diagnosis tips.

## Generate a feature to test your new cookbook ###
Define an appropriate Background section for the feature. Background can also ensure cookbooks/roles/databages are uploaded to the test chef server, so ensure you update the cookbook under development as part of the testing.

Create failing scenarios that define what the cookbook is intended to accomplish.

Run and see failures.

Work to make them pass.
