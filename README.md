# Drupal Deploy Scripts in Gradle

## Requirements

* Java
* Gradle

## Usage

Review your environment properties settings.  The example below uses `dev.properties`.

Create a properties file containing site specific settings called `site.properties`

and run:

    gradle deployDrupal -Denv=dev -Dsite=site -Dsrc=$WORKSPACE/src -Dworkspace=$WORKSPACE -DBUILD_NUMBER=$BUILD_NUMBER

The above line is suitable for pasting into a jenkins job's "switches" input box.

