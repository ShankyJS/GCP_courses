Cloud Computing has five characteristics:

- On-deman self-service: NO human needed.
- Resources are accessed from anywhere over the network: Broad Network Access.
- Resource pooling: Provider shares resources to consumers and exists all over the world.
- Rapid elasticity.
- Measured service: You pay for what you use.

An IT infrastructure is like a "city infrastructure".

People are Users.

Bikes, cars are applications. 

Streets, buildings and lights are Infrastructure (this is what GCP Provides).

# Cloud Vs Traditional Architecture. 

Cloud Computing is a continuation of a long-term shift in how computing resources are managed, you can rent out computing infrastructure and have it managed by professionals.

Why is google doing cloud? 

1980s: First wave, servers on-premise. YOU own everything, it's yours to manage.
2000: Second Wave: Datacenters, you pay for the hardware but rent the space. Stills yours to manage.
2006: First generation of Cloud Virtualized Data Centers, you rent the hardware and space but still control and configure virtual machines and pay for what you provision.
2009: Third wave managed service: Completely elastic storage, processing and machine learning so that youc an invest your energy in great apps. Pay for what you use. Google was well positioned on this wave.

Google believes every company is a data company. Create software is centered on Data, so every company will become an Data Company.

Google has one of the world's largest corporate purchasers of renewable energy. 100% carbon neutral since 2007. First data centers to achieve ISO 14001 certification.

# IaaS, PaaS and SaaS.

## IaaS

Infrastucture as a Service

The service provides the underlying architecture for you to run your services. The resources are provided but is up to the user to manage the operating system and the application.

- CPU, memory, storage and networking is provided as a service.
- THe user needs to manage the OS and the application.

This is Compute Engine.

## PaaS

Platform as a Service

The entire environment is managed by the user, and all that is required for us is to manage the applications, the operating system layer is managed by the service.

This is AppEngine.

## SaaS

Software as a Service

Infrastucture, platform and software are managed by the platform, you just need to bring your data, an example of this could be sales force. 


![](image-ksghfp2q.png)

# Google Cloud Architecture

GCP offers a range of compute services.
 
## Compute:

Includes virtual machines via compute engine.
Docker containers using GKE.
Deploying applications in a managed platform like AppEngine.
Running event serverless code using Cloud Functions.

## Storage:

For unstructured storage there is Cloud Storage.
For managed relational databases CloudSQL or CloudSpanner.
And for NoSQL there is Cloud Datastore or Cloud BigTable.
 
## BigData and Machine Learning

Managed services for BigData and Machine Learning are available, cable network spans the globe, they are connected over the 40% of world network by Google Network. And it's still growing, they want to provide the lowest latency and the highest througport. 

The network interconnects with the public internet with more than 90 internet exchanges and +100 presences worldwide.

Google has multiple edge connections to provide low latency around the globe.


## Understanding Regions and Zones.

GCP devides the world in 3 regional areas.

Americas, Europe and Asia Pacific.

Next there are dived to regions which they are independet geographic areas on the same continent. Within a region there are fast network connectivity under 1m/s that is at the 95%. One of the regions in europe es europe-west2(London).

Then Regions are divided into Zones. They are Datacenters within the regions. Like europe-west2-a-b-c.

GCP has expanded across 61 zones, more than 200+ coutnries.

Zonal resources operate exclusively in a single zone. 

Zonal: Persistent Disks, GKE Nodes.
Compute Engine Instance, Persistent Disk.

If the zone is unavailable, the resources are going to be unavailable.

### Global Resources

Can be managed across multiple regions, these resources can improve the availability of the application, those includes VPC's, Loadbalancers, HTTP. 

This resources need to be in a project that is the logical organization that Google uses.

Zones/Regions phisically organizes resources you use.
Projects organizes resources from the logical side.

Projects can be created, managed, deleted or recovered from accidential deletions.

Resources have hierarchy so they have to be unified by unique project_id and project_name. These are fixed values.

Projects can belong to a folder that is another kind of group herarchy.

You can nest folders into folders.

- Project: Store Front > Team1 Folder > Departament Folder1-2.
- Organization is the higher level of the hierarchy, this require us to us folders.

## Summary

So what's the cloud anywhay?

Cloud Computing reffers to Software and Services that runs on the Internet instead of locally in a computer, the advantage  is that you can access your information within any device with internet connection.

Because the servers manages CPU/memory and processing you don't need high end hardware to use services in the cloud.

Cloud Computing has five fundamental attributes:
- On demand self-service
- Broad network access
- Resource pooling
- Rapid elasticity 
- Measured Services

An IT infrastructre can be compared to a city infrastructure.

Cloud Computing is a continuation of a long-term shift in how computing resources are managed.

IaaS, PaaS and SaaS with increasing levels and choices of managed services.

GCP offers a wideee range of services.

GCP DIVIDES THE WORLD INTO REGIONS and zones.

The GCP resources you use,no matter where they reside, must belong to a project.