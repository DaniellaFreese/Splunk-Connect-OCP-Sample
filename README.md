# Install Splunk Connect on OCP
Purpose of this repo is to provide a rudimentary parameters required for deploying Splunk-Connect 1.4.10 on Openshift 4. 
This was validated on OCP 4.6 cluster. 

These notes were built for splunk-connect release version: 1.4.10 

### Pre-requisites
The following pre-requisites are required: 

Download Helm 3 
  To Download Helm 3 from Openshift 4 Console 
   * Login to OCP >> Top Right corner >> ? >> Command Line Tools >> Download Helm 3
   * 

Download the Splunk Connect Helm Chart. 
   * Github Link: https://github.com/splunk/splunk-connect-for-kubernetes

   * Couple ways to do this: 
        1. Add Helm Chart to your local repository: 
            `$ helm repo add splunk https://splunk.github.io/splunk-connect-for-kubernetes/`
        2. Download the helm chart with git pull 
        3. Download the helm chart as a zip 

Create a Index and HEC Token in Splunk to publish logs. Further details in the Splunk-Connect Github Documentation
`One events index, which will handle logs and objects (you may also create two separate indexes for logs and objects).`


### Prep the Helm Chart Values.yaml
A values.yaml that functions on openshift has been provided in this repo. Please modify further for your needs by reviewing the Splunk-Connect Documentation. Some sample of parameters to modify: 
* Splunk Details 
  * HEC Token 
  * Certificates 
* Container Logs
  * OCP Audit Logs 
  * Exclude certain container logs 
* Enable Events and Metrics logs 


### Install Splunk-Connect on openshift Cluster 
Log into the openshift cluster

Create a namespace to deploy splunk-connect application: `oc new-project splunk-connect`

Run Helm install to deploy splunk-connect to the new namespace: 
* if running the chart from local repo: `helm install splunk-connect splunk/splunk-connect-for-kubernetes -f values.yaml`
* if the chart has been downloaded: `helm install splunk-connect ./splunk-connect-for-kubernetes -f values.yaml`
  


