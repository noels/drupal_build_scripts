# Drupal Deploy Scripts in Gradle

## Requirements

* Java
* Gradle
* The user running the script must have permission to write to `.gradle/`

## Source Control

These scripts are deliberately source-control-agnostic. Use jenkins/whatever to check out the source, and point these
scripts at it.

## Templates and Properties

The templates folder contains two templates, one for a generated Drupal settings file and another for an Apache
vhost file. You can add new properties by surrounding them with @: `@property@`. The values of these properties
are automatically pulled from `*.properties` files.

Properties files are loaded in the following order:

* `secure.properties` (secure properties, like passwords you don't want checked in, go here) 
* `<site>.properties`
* `<environment>.properties`
* And finally, the default `build.properties`

Properties can't be overridden, so put the most specific things in earlier loaded files. i.e. 
secure overrides everything, site overrides environment and default, and environment overrides default.

There is nothing special about site or environment properties.  The names are specified on the command like this: 

    -Denv=dev -Dsite=site

or defined by system environment variables.

## Tasks

There are two "interesting" tasks.  deployDrupal and installDrupal.  installDrupal runs drush site-install so it will 
trash any existing install you have.  deployDrupal generates settings, packages up the code deploys it and restarts 
services.

an example to deploy the drupal site, "site" to a "dev" environment is:

    gradle deployDrupal -Denv=dev -Dsite=site -Dsrc=$WORKSPACE/src -Dworkspace=$WORKSPACE -DBUILD_NUMBER=$BUILD_NUMBER

The above line is suitable for pasting into a jenkins job's "switches" input box.

