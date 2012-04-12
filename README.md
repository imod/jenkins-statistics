Jenkins Usage Statistics
========================

Theses script are meant to create the underlying json's used to show the plugin statistics on the plugin info pages at jenkins-ci.org.
The json files are used by the confluence plugin ('hudson-plugin-info' - https://github.com/jenkinsci/backend-jenkins-plugin-info-plugin)


HOWTO
-----

1. download and unpack the raw data (*.json.gz) from from 'https://www.jenkins-ci.org/census/'

   $> groovy download.groovy [pwd]

2. collect the data from the raw json format and store it into a local SQLight database
   ... you might have to increase the memory: export JAVA_OPTS="-Xmx4000M -Xms4000M"

   $> groovy collectNumbers.groovy

3. generate the fine grained data set (json) for each plugin

	$> groovy createJson.groovy

The final json files will be in [worksapce]/target/stats - these files have to be uploaded to a webserver to make them available for the confluence plugin.


All the scripts can be reexecuted in case a failure happens, e.g. the download will only download the files he needs and collecting the numbers will only happen on the raw data which is not imported yet.