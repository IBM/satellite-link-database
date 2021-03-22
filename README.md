# satellite-link-database

In this tutorial you will learn, how to link a database service on IBM Cloud to your IBM Cloud Satellite location and verify the connection by sending the data to store.

# [Title]

## Introduction
State the purpose of your tutorial, your intended audience, and the benefits readers can gain from it. Aim to grab the reader’s interest quickly, using terms they are likely to search on and relate to.

## Prerequisites
List or describe any skills, tools, experience, or specific conditions required to perform the tutorial. Include version levels for any required tools or platforms. Include links to necessary resources whenever possible.

## Estimated time
Provide guidance on how long it will reasonably take to complete the steps under normal circumstances.

## Steps

#### 1. Create a Satellite location in IBM Cloud.

- From the [Satellite Locations dashboard](https://cloud.ibm.com/satellite/locations), click Create location. A location represents a data center that you can fill with your own infrastructure resources to run IBM Cloud services or other workloads on your own infrastructure.
- Enter a name and an optional description for your location.
- Select the IBM Cloud region that you want to use to manage your location. For more information about why you must select an IBM Cloud region, see [About IBM Cloud regions for Satellite](https://cloud.ibm.com/docs/satellite?topic=satellite-sat-regions#understand-supported-regions). Make sure to select the region that is closest to where your host machines physically reside that you plan to add to your Satellite location to ensure low network latency between your Satellite location and IBM Cloud.
- Click Create location. When you create the location, a location master is deployed to one of the zones that are located in the IBM Cloud region that you selected.

#### 2. Attaching hosts from on-premises data centers and edge networks

- Hosts are machines that reside in your infrastructure In your on-premises environment, identify or create at least three host machines in physically separate racks, which are called `zones` in Satellite, that meet the [minimum hardware requirements](https://cloud.ibm.com/docs/satellite?topic=satellite-host-reqs).

- Follow the steps in this [link](https://cloud.ibm.com/docs/satellite?topic=satellite-getting-started#gs-attach-hosts-onprem) to attach hosts from on-premises data centers and edge networks. 

#### 3. Assign hosts to the Satellite location control plane

- From the actions menu of each host machine that you attached, click `Assign host`.
- For the Cluster, select `Control plane`.
- For the Zone, select a unique zone such as `zone-1`.
- Click `Assign host`. 
>>NOTE: When you assign the hosts to the control plane, IBM bootstraps your machine. This process might take a few minutes to complete. During the bootstrapping process, the Health of your machine changes from Ready to Provisioning.
- Repeat these steps for each host. Make sure that you assign each host to a different zone so that you spread all three hosts across all three zones, such as `zone-1`, `zone-2`, and `zone-3`.
- From the Hosts tab, verify that your hosts are successfully assigned to the Satellite control plane. The assignment is successful when an IP address is added to your host and the Health status changes to Normal.

#### 4. Create PostgreSQL database and link it to IBM Cloud Satellite

A cloud endpoint allows you to securely connect to a service, server, or app that runs outside of the location from a client within your Satellite location.

<b>Create the Service</b>
- Here we create IBM DB2 on cloud database service to store the data.

- Create a [Databases for PostgreSQL](https://cloud.ibm.com/catalog/services/databases-for-postgresql) service.

- Choose `Databases for PostgreSQL`. Click on `Create`.

- Name your database and click on `Create`.

- Once the service is ready, click on "Service credentials" in the navigation pane and select the "New credential" option and create credentials. Copy `Host` url and `Port` number. .

- These service credentials will be used to create an Endpoint Link for the Satellite location.

<b>Link the Service to your satellite</b>
- Click on `Link Endpoints` tab.
![](images/p1.png)

- Click on `Create on Endpoint` as shown below.
![](images/p2.png)

- Select `Cloud` and click on next.
![](images/p3.png)

- Enter an `Endpoint name`. In `Destinaion URL or IP` paste the host name that you copied when you created the Db2 service cerdentials . In `Destination port` paste the port number that you copied when you created Db2 service credentials.
![](images/p4.png)

- Leave the default value and click on `Next` as shown below.
![](images/p5.png)

- Click on `Create endpoint` as shown below.
![](images/p6.png)

- It takes few moments to create an endpoint. Once the endpint is created, you can view it under Endpoints as shown below.
![](images/p7.png)

#### 5. Create the OpenShift Cluster that will live on your satellite location

- Here we create the OpenShift cluster that will live on your satellite location. 

- Follow the steps in this [link](https://cloud.ibm.com/docs/satellite?topic=openshift-satellite-clusters#satcluster-create-console) to create OpenShift clusters on Satellite from the console.

- Now you can deploy an application that takes in data from the IoT sensors and data from CCTVs in your factory environment, send that data to IBM Watson services for processing and store it in Db2 database. All of this in your location. This way you can reduce latency and effectively warn someone if they are found without safety gear.

#### 6. Send data to PostgreSQL database using the Satellite endpoint

- Copy the `Satellite endpoint` link that you created in step 4.

- Copy the `username` and `password` from the credentials that you created in step 4. 

- Paste the above copied parameters in the notebook.

- Run the notebook.

![](images/satellite.png)

## Summary

With IBM cloud satellite you can quickly address unforeseen challenges, leverage cloud benefits in any location and innovate quickly anytime anywhere.

State any closing remarks about the task or goal you described and its importance. Reiterate specific benefits the reader can expect from completing your tutorial. Recommend a next step (with link if possible) where they can continue to expand their skills after completing your tutorial.

## Related links
Include links to other resources that may be of interest to someone who is reading your tutorial.
