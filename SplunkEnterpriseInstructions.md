# Testing Splunk-Connect Openshift Configuration 

## Running Splunk Enterprise Docker Image - Trial 
For testing purposes I will spin up Splunk Enterprise as a Docker image to trial and validate my integration. For rapid testing purposes, the docker container is so easy to setup, it's easier just to run the container via docker than to leveraging to splunk operator. 

For this sample you'll need to have docker running on your local machine. 

We'll go ahead and pull down the image, and start the container with: 
```
$ docker pull splunk/splunk:latest
$ docker run -d -p 8000:8000  -p 8088:8088 -e "SPLUNK_START_ARGS=--accept-license" -e "SPLUNK_PASSWORD=<password>" --name splunk splunk/splunk:latest
```
Here is the link to dockerhub for more information regarding the [splunk image](https://hub.docker.com/r/splunk/splunk/)

If you need to tunnel to the server please run the following command:
`sudo ssh   -L 8000:localhost:8000 <user>@<hostname>`


When splunk enterprise is up, you should be able to navigate to it on the browser on localhost:8000

## Setup HTTP Event Collector (HEC) Token in Splunk 

Login to Splunk with admin account 
Settings >> Data Inputs >> HTTP Event Collector >> New Token 
Select Source Page Inputs: 
1. fill in the name 
2. do not toggle Enable indexer acknowledgement 
   
Input Settings Page: 
1. add one index to "selected items" box (or create a new index and add it to the selectd items box)

Review & Submit --> retrieve your HEC Token
Default connections details will be: 
```
    indexName: <index-name>
    host:  <hostname>
    token: <hec-token>
    port: 8088
    protocol: https
    insecureSSL: true
```







