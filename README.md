Gilead - GSA Filesystem Connector
=======

This repository contains all code used to build the GSA Filesystem Connector that includes the Custom Date Formatting Updates for Gilead Sciences.

Base Filesystem Connector version: v4.1.0

## Requirement
By default, the File System Connector indexes any value contained within any metadata field as it appears. Dates are a standard data type, however they are communicated in a variety of formats depending upon filetype. Because Gilead is indexing multiple file types and content sources within their search index, the desire to normalize the formatting of date values has arisen. Therefore, the Custom Date Formatting Feature shall identify date values expressed in three (3) particular formatting patterns within particular file types to be re-written prior to indexing.

Target date format: 
* 2014-08-22T11:05:31-07:00

Formats to be updated:
* D:20121219093655-08'00'
* 18/12/2012 17:4:44
* D:20031104134656

## Success Criteria

The Application shall be deemed acceptable if it meets the following criteria:
* Existing metadata with dates are retained
* CreationDate and ModDate are processed for formatting
* Formatted dates are saved in two new metadata: CreationDate_formatted, ModDate_formatted
* Formatted dates are shown in search results (requires front-end change)

## Build Instructions
1. Install [Ant](http://ant.apache.org/)
2. Download source code

  ```
  git clone -b gsa-filesystem-gilead https://github.com/sadasystems/filesystem --single-branch gsa-filesystem-gilead
  ```
3. Go to the folder of the downloaded sources

  ```
  cd gsa-filesystem-gilead
  ```
4. Create jar file
  ```
  ant -Dadaptor.version=<VERSION> -Dtika.jar=<TIKA_JAR_LOCATION> dist
  ```
  *Note:* 
  * *If adaptor.version is not provided, the current date will be used as adaptor suffix. Example: adaptor-fs-20160927-withlib.jar*
  * *If tika.jar is not provided, the current Tika jar file in the lib folder (tika-app-1.13-dateformat.jar) will be used. Get the latest tika app for gilead from https://github.com/sadasystems/tika/tree/gsa-tika-gilead*
  
5. Generated jar file will be inside the **dist** folder. Use the *adaptor-fs-\<VERSION\>-withlib.jar*

## Deployment Instructions
1. Download the Filesystem v4.1.0 installer

2. Follow the installation instructions in the [Filesystem Connector v4.1.0 documentation]( https://static.googleusercontent.com/media/www.google.com/en//support/enterprise/static/gsa/docs/admin/connectors/40/410/DeployingtheConnectorforFileSystems.pdf)

  *Note: Do not start the connector yet*
3. Replace the adaptor jar file with new one: *adaptor-fs-\<VERSION\>-withlib.jar*

4. Open **adaptor-config.properties** file and add a entry for the target date format. 
  ```
  filesystemadaptor.dateFormat=yyyy-MM-dd'T'HH:mm:ssXXX
  ```
  
5. Run the connector as a service. Refer to the instructions in the [Administration Guide] (https://static.googleusercontent.com/media/www.google.com/en//support/enterprise/static/gsa/docs/admin/connectors/40/410/AdministrationGuideforGoogleConnectors.pdf)
