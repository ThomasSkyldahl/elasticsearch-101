#Setup and configuration#

**Assignments:**

1. Download and configure Elasticsearch following the guide below
2. try running Elasticsearch.bat	
	- verify by visiting [http://localhost:9200](http://localhost:9200) to see version information
3. try installing Elasticsearch as a Service
	- start the service and verify by visiting [http://localhost:9200](http://localhost:9200) to see version information


##Downloads##

Let's get started installing Elasticsearch

First of we have to download the lastest version of Elasticsearch from: [http://www.elasticsearch.org/overview/elkdownloads/](http://www.elasticsearch.org/overview/elkdownloads/)


We also need a JRE as Elasticsearch is based on Java (Yes I know its insane)

Download the latest version of the server JRE from 
[http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html)

***(Be aware that the save dialog removed the .tar in .tar.gz remember to add it again otherwise 7zip wont recognize the file type correctly)***

You can also use a normal JRE but you will get warnings and it doesn't perform as good as the optimized server JRE.

##Setup##

###Creating the folder structure###
***Unblock the downloaded files before proceeding*** 

I normally place Elasticsearch in the following structure 

- C:\search
	- elasticsearch-1.4.2 *<- this is the folder from the elasticsearch zip file*
	- jre *<- this contains the jre folder found inside the jdk folder*

###Environment variable###

To setup the **JAVA_HOME** environment variable

You can do it by running the following in a Powershell admin prompt:

    [Environment]::SetEnvironmentVariable("JAVA_HOME", "C:\search\jre\", "Machine")

I set it to a machine level variable as I want us to be able to install elasticsearch as a service at some point

###Change the default configuration###

open elasticsearch.yml inside the elasticsearch config folder

this file contains the default configuration some of the options can be overwritten on the index level if needed.

We need to uncomment the **cluster.name** setting a change it to something unique I use the following format **"elasticsearch-[version]-[machinename]"** 

*if this isn't configured in a environment with multiple instances of Elasticsearch running on the default name "elasticsearch" cluster name the machine would join the cluster*

####Other options ####

Its also good to know the following settings

    index.number_of_shards: 5
    index.number_of_replicas: 1

The default setting is to split the index in 5 shards and have a single replica, this makes sense in most production environments, as it give the cluster room to grow.

But when running in DEV it makes sense to set configure it a little different Elasticsearch recommends running with the settings below in DEV

    index.number_of_shards: 1
    index.number_of_replicas: 0

##Running Elasticsearch##
to run elasticsearch you need to use the elasticsearch.bat inside the bin folder.

Open a admin console and run: 

    elasticsearch.bat


###Installing Elasticsearch as a Service###
inside the bin folder you will find a service.bat that can be used install Elasticsearch as a Service

you can run it with the following commands

    service.bat install
    service.bat remove
    service.bat start
    service.bat stop

*When running it on you DEV machine setup the account for the service to be System as our group policy blocks the service from running after reboots*
