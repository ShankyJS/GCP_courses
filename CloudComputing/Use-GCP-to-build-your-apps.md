# Compute Options of the Cloud.

GCP Offers a variety of cs 
for general workloads that requires dedicated resources for your application Compute Engine (IaaS / Virtual Machines with industry leading price/performance.

For platform as a Service, App Engine is a good option. Zero ops platform for building highly available apps.

For Serverless Logic we can use Cloud Functions a lightweight fully maanaged serverless execution environment for building and connecting cloud services.

For Hybrid workloads we can use GKE cluster manager and orchestration engine built on Google's container experience.


# Exploring IaaS with Compute Engine.

Compute engine delivers virtual machines running in Gooogle data centers, compute engine is ideal if you need complite control in your VM infrastructure, make changes to Kernel, providing your own network and graphics drivers of if you need to run packages that can't be containarized.

Compute Engine is an Infrastructure as a Service.
Scalable, high-performance VMs.
Runs any computing workload.
Virtual servers are available in many custom machine types, distros etc.
Windows or Linux
No upfront investment required.

The purpose of Custom Machines is that you can run your application but none of the predefined versions meets your requirements, or GPU is needed, etc. Custom virtual machines makes you available to create exactly what you need.

- Higher proportion of memoriy to CPU
- Higher proportion of CPU to Memory
- Blend or Both

## Building virtual disks.

Network storage can be attached to VMs as persistent disks (PDs).
PDs are cost effective, durable and offer good performance.
Local SSDs provide higher performance with lower latency, but exist only for the lifetime of a specific instance.
Standard PD throughput performance and IOPS increases linearly with the size of the disk until it reaches set per-instance limit.
SSD PD IOPS performance dependso n the number of VCPUS in the instance in addition to disk size.

## Compute engine and Networks.

Networks in the cloud are very similar to the local network.

You can:

Inbound/outbound firewall rules.
Create static routes.
Scale and distribute applications using Cloud Load Balancing.
Global and multi-regional subnetwork.

Subnets works segmenting your cloud network IP space, the prefixes can be automatically allocated or you can create topologys custom.

When you build a Compute Engine you use a virtual network adapter that is part of the instance to connect the VM to the Network, you can have up to 8 virtual adapters for compute engine.

Subnets and cloud loadbalancing helps to network.

# How autoscaling works.

Autoscaler controls instances groups, adding and removing instances using policies, includes the minimum and maximum quantity of instance replicas.

A template can be used to identify images services and startup new VMs.

Target CPU utilization = 0.75

1. Actual utilization = 385 / 400 = 96.25%
2. If +1 then 385/500 = 77% (Still above target 75%)
3. If +2 then 385/600 = 64.16%.
0
Actual utilization = 330/600 = 55%
If -1 then 330/550 = 66% (Still below target).
If -2 then 330/400 = 82.5%

# Exploring PaaS with AppEngine.

AppEngine allows highly scalable application in a fully managed serverless platform, is highly value to be able to write code without having to touch servers, clusters or whatever.

AppEngine allows high availability without complex application.

As a fully managed env appEngine is a perfect example as a Platform as a Service, saves cost, time in software application development eliminating needs of OPS.

- No need to buy, build or operate hardare/infrastucture.
- No managing servers or configuring deployments.
- Focus on app development instead of operations.
- Use a range of languages and tools.
- Let's you manage from your CLI using CloudSDK, you can use visual studio and powershell.
- Automatic scaling according to the use when the code is running.

App Engine offers two different envs.

Standard environment & Flexible environment, you can use both at the same time.

## Standard environment
- Fully managed
- Scalled to zero.
- Specific versions of supported languages.
- Changes configuration limited.

## Flexible environment.

- Docker container support.
- VMs exposed.
- Any language in your container.
- More options for infrastructure customization and configuration for performance.

An App Engine architecture example.

PC -> Cloud Balancing > FrontEnd deployed to AppEngine -> Uses dynamic storage Cloud Datastore > CloudSQL and interconnects with a Batch Application running in AppEngine (Backend).

App Engine addresses the key needs of developers.

- Multiple storage options.
- Automatic scaling
- Loadbalancing in single or multiple regions close to users to make it highly available.
- App Versioning which includes creating dev, testing and prod envs.
- Monitoring and logging (stackdriver)
- Security.

# Build apps at High scale with GAE.

Enter the following command to copy the Hello World sample app repository to your Google Cloud instance:

````
gsutil -m cp -r gs://spls/gsp067/python-docs-samples .

````
Go to the directory that contains the sample code:

````
cd python-docs-samples/appengine/standard_python3/hello_world
````

Now deploy the code.

````
gcloud app browse
````

# Event driven Programs with Cloud Functions.

Developer agility comes from building systems composed on small and independent units of functionality focused on doing one thing well, Cloud Functions let's you build and deploy services at the level of a single function, not at the level at entire VMs or Cluster.
- It's ideal if you want to connect cloud services automated with event driven function that responds to cloud events.
- It's ideal if you want to use Open and familiar NodeJS, Python and Go without managing a runtime.
- Cloud functions provides a connective layer of logic that let's you write code to connect and extend Cloud Services.
- You can listen and respond to a file upload to cloud storage, a log change or an income message to a topic.
- Have access to GCP IAM to authenticate with tons of services.
- Events ocurrs and you can create events response with triggers in a set of events, binding a function to a trigger captures an act on events.
- Cloud functions can scalate from 1 invoke to millions with any action neeeded.

## How cloud functions works.

Cloud Services -> Emits events > Cloud Functions responds to events -> Invokes other services and call other APIS.

# Cloud Functions lab.

Copy the following code to a file index.js.

````
/**
* Background Cloud Function to be triggered by Pub/Sub.
* This function is exported by index.js, and executed when
* the trigger topic receives a message.
*
* @param {object} data The event payload.
* @param {object} context The event metadata.
*/
exports.helloWorld = (data, context) => {
const pubSubMessage = data;
const name = pubSubMessage.data
    ? Buffer.from(pubSubMessage.data, 'base64').toString() : "Hello World";

console.log(`My Cloud Function: ${name}`);
};
````

Create a bucket:

````
gsutil mb -p $PROJECT_ID gs://my_function_bucket
````

Create the function.

````
gcloud functions deploy helloWorld \
  --stage-bucket my_function_bucket \
  --trigger-topic hello_world \
  --runtime nodejs8
````

Testing the function:

````
DATA=$(printf 'Hello World!'|base64) && gcloud functions call helloWorld --data '{"data":"'$DATA'"}'
````

Read the logs:

````
gcloud functions logs read helloWorld
````

# Containerizing and Orchestrating Apps with GKE.

## IaaS to PaaS comparison

IaaS -> Compute Engine (Pay for what you allocate and servers, networking storage).
Google Kubernetes Engine -> In the middle.
PaaS -> App Engine (Pay for what you use, preset run-times, managed services).

## Where GKE fits within GCP

GKE is ideal when for those that are challenged to people managing a fleet of VM's and containers it's determined as a Solution, in order to containarized and don't have dependencies of kernel changes or non-linux operation systems.

GKE does not need to ever touch a server or infrastructure.

IaaS virtualizes the hardware.

App > Libs > OS > Hypervisor Hardware. 

(Each developer can manage the hardare, runtimes and libraries, partitions of ram, networking interfaces and so on.)

Virtualizing the hardware costs time and resources.

If you need to scale you need to copy a whole VM and that can be costly and slow.

### PaaS gives access to hosted programming services.

Provides hosted services and an environment that can scale workloads independently all you do is:

- Write your code in self-contained workloads and include any libraries.
- Decouple code easily because their tied to the underlying hardware, operating systems or the stack that you used to manage.

#### The platform scales to meet demand.

- Build your apps as decoupled microservices.
- You may not be able to fine-tune the underlying architecture to save costs.

And that is where containers coming. 

The idea of the containers is to give the independent scalability of workloads in a Platform as A service in an abstract layer of the operating system and hardware in an Infrastructure as a Service.

It's just requires a few system calls to create and start quickly as a process all you need is a kernel that supports containers and container runtime like containerd or docker.

In essence you are virtualizing the operating system, scales as Platform as a Service but gives you nearly the same flexibility as an Infrastructure as a Service.

## Deploying multiple containers on servers.

You can scale multiple containers depending of the size of your workload with a few actions.

The hosts can scale up/down and stop and start containers on demand.

You can build containers and hosts independently for maximun eficiency and savings.

Kubernetes is an open source container orchestration tool you can use to simplify the management of containarized environments. You can run it as a hosted service in GCP or in your own VM's. 

# Deploy GKE. Lab

Set compute zone

````
gcloud config set compute/zone us-central1-a
````

Create my new cluster.

````
gcloud container clusters create my-new-cluster
````

Get the credentials

````
gcloud container clusters get-credentials my-new-cluster
````

Deploy a workload:

````
kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
````

Expose it using a Kubernetes service to external traffic.

````
kubectl expose deployment hello-server --type=LoadBalancer --port 8080

````

Delete your kubernetes cluster

````
gcloud container clusters delete my-new-cluster
````

# Set up Network and HTTP Load balancer

What you'll do:

- Set up a network load balnacer.
- Set up an HTTP load balancer.
- Get hands-on experience learning the differences between network load balancers and HTTP load balancers.


Config zone and region.

````
gcloud config set compute/zone us-central1-a
gcloud config set compute/region us-central1
````

Create three new virtual machines in the default zone giving them all the same tag. With the tag we will match the firewall policy.

````
gcloud compute instances create www1 \
  --image-family debian-9 \
  --image-project debian-cloud \
  --zone us-central1-a \
  --tags network-lb-tag \
  --metadata startup-script="#! /bin/bash
    sudo apt-get update
    sudo apt-get install apache2 -y
    sudo service apache2 restart
    echo '<!doctype html><html><body><h1>www1</h1></body></html>' | tee /var/www/html/index.html"
    
gcloud compute instances create www2 \
  --image-family debian-9 \
  --image-project debian-cloud \
  --zone us-central1-a \
  --tags network-lb-tag \
  --metadata startup-script="#! /bin/bash
    sudo apt-get update
    sudo apt-get install apache2 -y
    sudo service apache2 restart
    echo '<!doctype html><html><body><h1>www2</h1></body></html>' | tee /var/www/html/index.html"
    
gcloud compute instances create www3 \
  --image-family debian-9 \
  --image-project debian-cloud \
  --zone us-central1-a \
  --tags network-lb-tag \
  --metadata startup-script="#! /bin/bash
    sudo apt-get update
    sudo apt-get install apache2 -y
    sudo service apache2 restart
    echo '<!doctype html><html><body><h1>www3</h1></body></html>' | tee /var/www/html/index.html"
````

And then create the firewall rule to allow external traffic to the VM instances.

````
gcloud compute firewall-rules create www-firewall-network-lb \
    --target-tags network-lb-tag --allow tcp:80
````

Create a static external IP address for your load balancer

````
gcloud compute addresses create network-lb-ip-1 \
 --region us-central1
````

Add an http legacy health check resource:

````
gcloud compute http-health-checks create basic-check
````

Add a target pool in teh same region as the instances, running the target pool using health check which is required for the service to function.

````
gcloud compute target-pools create www-pool \
    --region us-central1 --http-health-check basic-check
````

Add my instances to the pool:

````
gcloud compute target-pools add-instances www-pool \
    --instances www1,www2,www3
````

Add the forwarding rule to redirect to port 80 always.

````
gcloud compute forwarding-rules create www-rule \
    --region us-central1 \
    --ports 80 \
    --address network-lb-ip-1 \
    --target-pool www-pool
````

View the external IP address of the www-rule forwarding rule used by the load balancer.


````
gcloud compute forwarding-rules describe www-rule --region us-central1
````

Generate traffic with CURL and see the responses, you will see that all the VM's responds.


````
while true; do curl -m1 34.135.3.82; done
````

## Create an HTTP load balancer

HTTP(s) load balancing is implemented on Google Front End, you can configure URL rules to route some urls to one set of instances and route other URLs to other instances.

To create a load balancer with a Compute Engine backend, your VMs need to be in an instance group. The managed instance group provides VMs running the backend servers of an external HTTP load balancer. For this lab, backends serve their own hostnames.


Let's create the load balancer template.


````
gcloud compute instance-templates create lb-backend-template \
   --region=us-central1 \
   --network=default \
   --subnet=default \
   --tags=allow-health-check \
   --image-family=debian-9 \
   --image-project=debian-cloud \
   --metadata=startup-script='#! /bin/bash
     apt-get update
     apt-get install apache2 -y
     a2ensite default-ssl
     a2enmod ssl
     vm_hostname="$(curl -H "Metadata-Flavor:Google" \
     http://169.254.169.254/computeMetadata/v1/instance/name)"
     echo "Page served from: $vm_hostname" | \
     tee /var/www/html/index.html
     systemctl restart apache2'
````

Create a managed instance group based on the template:

````
gcloud compute instance-groups managed create lb-backend-group \
   --template=lb-backend-template --size=2 --zone=us-central1-a
````

Create the fw-allow-health-check firewall rule. This is an ingress that allows traffic from the Google Cloud Health checking systems (130.211.0.0/22) and 35.191.0.0/16) with allow-health-check tag we are identifying the VMs.

````
gcloud compute firewall-rules create fw-allow-health-check \
    --network=default \
    --action=allow \
    --direction=ingress \
    --source-ranges=130.211.0.0/22,35.191.0.0/16 \
    --target-tags=allow-health-check \
    --rules=tcp:80
````

Now that the instances are up and running let's set a global static external IP address.

````
gcloud compute addresses create lb-ipv4-1 \
    --ip-version=IPV4 \
    --global
````

The IP is now reserved.

````
 gcloud compute addresses describe lb-ipv4-1 \
>     --format="get(address)" \
>     --global
````

Create a heltcheck for the loadbalancer

````
gcloud compute health-checks create http http-basic-check \
        --port 80
````

Creatge a backend service.


````
cloud compute backend-services create web-backend-service \
    --protocol=HTTP \
    --port-name=http \
    --health-checks=http-basic-check \
    --global
````

add your instance group as the backend to the service.

````
gcloud compute backend-services add-backend web-backend-service \
    --instance-group=lb-backend-group \
    --instance-group-zone=us-central1-a \
    --global
````

Create a URL map to route the incoming requests to the default backend service.

````
gcloud compute url-maps create web-map-http \
    --default-service web-backend-service
````

Create a target HTTP proxy to route requests to your URL map:

````
gcloud compute target-http-proxies create http-lb-proxy \
    --url-map web-map-http
````

Create a a global forwarding rule to route incoming requests to the proxy.

````
gcloud compute forwarding-rules create http-content-rule \
    --address=lb-ipv4-1\
    --global \
    --target-http-proxy=http-lb-proxy \
    --ports=80
````


# Summary

There are four different compute options i nthe Cloud to chose from: 

Compute ENgine, App Engine, Clodu FUnctions, and GKE.

Compute Engine (an infrastructure as a service) delivers virtual machiens via Google's data centers and global fiber network.

Autoscaling controls managed instanced groups.

AppEngine is computing platform provided as a service allowing users to write better code.

Cloud Functions is a serverless options that connects and automates.

GKE is a hybrid between cCompute Engine (IaaS) and App Engine (PaaS).