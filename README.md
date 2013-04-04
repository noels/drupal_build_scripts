Templates and Properties

In templates folder you will find two templates.  One for a generated Drupal settings file and another for apache 
vhost.  You can put any new property by surronding it in @ like: @property@.  The value of these properties are
automatically pulled from .properties files. 

Properties files are loaded in the following order: 
secure.properties (where unchecked in passwords go) 
<site>.properties, 
<environment>.properties, 
then the default build.properties

Once a property is set, it can't be changed, so put most specific things in earlier loaded files. i.e. 
secure overrides everything, site overrides environment and default, and environment overrides default.

There is nothing special about site or environment properties.  The names are specified on the command like this: 
-Denv=dev -Dsite=site
or defined by system environment variables.

Tasks
There are two "interesting" tasks.  deployDrupal and installDrupal.  installDrupal runs drush site-install so it will 
trash any existing install you have.  deployDrupal generates settings, packages up the code deploys it and restarts 
services.

and example to deploy the drupal site, "site" to a "dev" environment is:

gradle deployDrupal -Denv=dev -Dsite=site -Dsrc=$WORKSPACE/src -Dworkspace=$WORKSPACE -DBUILD_NUMBER=$BUILD_NUMBER

The above line is suitable for pasting into a jenkins job's "switches" input box.

The build scripts don't care about your souce control. Deliberately. Use jenkins/whatever you like to check out your
source and simply point the build scripts to it.




