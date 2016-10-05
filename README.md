Gilead - GSA Filesystem Connector
=======

This repository contains all code used to build the GSA Filesystem Connector that includes the Custom Date Formatting Updates for Gilead Sciences.

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
git clone https://github.com/sadasystems/filesystem/tree/gsa-filesystem-gilead
```
3. Go to the folder of the downloaded sources
```
cd gsa-filesystem-gilead
```

3. Create jar file
```
ant dist 
```

## Deployment Instructions
1.

