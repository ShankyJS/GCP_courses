# The Purpose of APIs

An API is a software structure written so presents a clean interface that abstracts away needless details API's are used to simplify the way different disparate software resources communicate by using a universal structure of communications we open wide opportunities.

Representational State Transfer `REST` is currently the most popular architectural style for surfaces.

## REST

- Outlines a currently set of constraints and agreements that the service needs to complain with, if the service complains its said that it's restful.
- AN API that uses HTTP requests to GET, PUT, POST and DELETE data. API is intended to be deployed in architectural structure that scales well and applies  them to services, these apis intended to spread widely to consumers and deployed to devices with low computing resources like mobile, are well-suited to a REST structure. It uses HTTP requests.
- Designed to set up a format for applications to communicate.
- Great for cloud applications because they are stateless. No data needs to be stored or referenced for the API to run.
- Authentication can be done by Oauth and security can be used by leveraging tokens.

## Deploying and Managing APIs can be Difficult. (API management)

- Interface Definition: Language or format to describe the service.
- Authentication and authorization: How you authenticate and authorize users that request your API.
- Management and scalability: How you ensure that your API scales to meet demand.
- Logging and monitoring: Wheter your infrastrucutre log details API invocations and provides monitoring metrics.

<br>

# Cloud Endpoints

A way to develop, deploy, manage API's on any Google Cloud Backend.

Cloud Endpoints is a distributed API management system, with that you can control who has access to your API, you can generate API keys in the GCP console and validate on every API call and share your API with other developers to allow them to generate their own keys.

- Validate CAlls with JSON web tokens.
- Identify app users with Auth0 and Firebase auth.

## Cloud Endpoints Features

### Speed

- ESP provides security and insight < 1ms.
- Automatic API deployment.

### Monitoring and logging

- Inspect performance with Stackdriver Trace.
- Real-time log management with Stackdriver logging
- Analysis with BigQuery.

### Integration.

- You can choose your own framework and language. (Or use GCP's open source SDK.)
- Upload an OpenAPI specification and deploy Google's containerized proxy.

## Where Cloud Endpoints fits.

Mobile and cweb client Applications > Connects to Cloud Endpoints > CE connects to Runtime environments (AppEngine, GKE, Compute Engine) and interconects Backend Services (GCS, CSQL, Cloud DS).

## Cloud Endpoints helps to deploy and manage API's.

- Interface Definition: Open API (gRPC API)
- Authentication and authorization: Service-to-service authentication, user authentication.
- Management and scalability: Stackdriver logging, stackdriver Trace.
- Logging and monitoring: Extensible Service Proxy, service management, service control.

<br>

# Cloud Endpoints: Qwik Start

````
# Get the code
git clone https://github.com/GoogleCloudPlatform/endpoints-quickstart
````

To publish a REST API to Endpoints, an OpenAPI configuration file that describes the API is required. The lab's sample API comes with a pre-configured OpenAPI file called openapi.yaml.

Endpoints uses Google Service Management, an infrastructure service of Google Cloud, to create and manage APIs and services. To use Endpoints to manage an API, you deploy the API's OpenAPI configuration to Service Management.

Cloud Endpoints uses the host field in the OpenAPI configuration file to identify the service. The deploy_api.sh script sets the ID of your Cloud project as part of the name configured in the host field. (When you prepare an OpenAPI configuration file for your own service, you will need to do this manually.)

````
gcloud endpoints services deploy openapi.yaml
````

## Deploying the backend.

````
./deploy_app.sh
````

This script creates an AppEngine Flexible environment in the us-central region with 

````
gcloud app create --region="$REGION"
````

## Sending requests to the API

````
curl "https://example-project.appspot.com/airportName?iataCode=SFO"
San Francisco International Airport
````

## Generating traffic

With APIs deployed with Cloud Endpoints, you can monitor critical operations metrics in the Cloud Console and gain insight into your users and usage with Cloud Logging.

Run this traffic generation script in Cloud Shell to populate the graphs and logs.

## Add quota to the API

Cloud Endpoints lets you set quotas so you can control the rate at which applications can call your API. Quotas can be used to protect your API from excessive usage by a single client.

````
./deploy_api.sh ../openapi_with_ratelimit.yaml
````

Redeploy app Engine to run with the new quotas:

````
./deploy_app.sh
````

### Create credential

Go to Api & Services > Credentials > API Key.

Export it:

````
export API_KEY=your_api_key
````

````
curl -H 'x-api-key: YOUR_API_KEY' "https://example-project.appspot.com/airportName?iataCode=SFO"
San Francisco International Airport
````


The API now has a limit of 5 requests per second. Run the following command to send traffic to the API and trigger the quota limit:

````
{
 "code": 8,
 "message": "Quota exceeded for quota metric 'airport_requests' and limit 'limit-on-airport-requests' of service 'qwiklabs-gcp-01-1c7a827a8609.appspot.com' for consumer 'project_number:1036433451940'.",
 "details": [
  {
   "@type": "type.googleapis.com/google.rpc.DebugInfo",
   "stackEntries": [],
   "detail": "internal"
  }
 ]
}
Quota exceeded.
````

# Using Apigee

Apigee it's a platform for developing and managing APIs with a proxy-layer. An API proxy is an interface to developers that uses your backend developers,

Rather than having devs consuming the API directly they access the Edge-api proxy that you create. With that you can add security, rate limiting, quotas, caching and persistence, analytics, full handleling.

Because the backend services of Apigee not needs to be in GCP, it can be used for Legacy. Instead to replacing a monolithic app in one risky move they can use Apigee Edge to peel of that services one by one. Implementing API's as a facade or adapter layer each consumer can invoke these moder's api's to retrieve information from the backend instead of implementing functionality to communicate using outdated protocals and different interfaces.

API Gateway can retrieve data from multiple services with a single request. You can use Cloud Endpoints to implement API gateways, and your applications can run in GCP backends.


/order endpoints > Cloud Endpoint > /account /history endpoints in GKE.

/payment endpoint > ApiGee > /creditgateway /rewards > In a Legacy App.

# Manage Message Services.

Across industry a common scenario is that org needs to rapidly ingest, transform and analyze massives amount of dataa.

A Gaming application might receive user engagement and click stream data.

In the Shipping Industry IoT applications might receive large amounts of sensors data from thousands of sensors. 

Data processing applications transform the ingested data and save it in an analytics database, then you can analyze the data to create business insights and create innovate user experiences.

Web > User and device data > Ingest > Transform > Analyze > User Experience > Android/web/iOS platform.

Organizations orchestrate complex processes.

## Example.

When a user plays a song, the music streaming services must perform many operations in the background, like.

- Perform live updates to the catalog.
- Update song recommendations.
- Handle add events.
- Provide analytics on user actions.

## Use cases for a managed messaging system.

- Balance workloads in network clusters: A hugh amount of work can be distributed amount multiple workers as CE instances, GKE.
- Implement asynchronous workflows: Order processing applications can place orders in a topic from which it can be processed by one or more workers distributing event notifications.
- Distribute event notifications: A service that accepts user signups our downstream services can subscribe to receive notifications of the event.
- Refresh distributed caches: An application can publish invalidation events to update the IDs of objects that have changed.
- Log to multiple systems: A compute engine can write logs to the monitoring system to a database for later querying and so on.
- Stream data from various processes or devices: Residential sensor can stream data to back-end servers hosted in the cloud.
- Reliability Improvement: A single zone compute engine service can operate in additional zones by subscribing to a common topic to recover from failures in the zone or region.

# Cloud Pub/Sub

Is GCP's managed message service. PubSub is a real time messaging service that allows you to capture data and rapidly pass massives amount of messages between other GCP services and other software applications.

Think of it like a connector that removes the time that you tipically spent managing operations.

## The main features of Cloud Pub/Sub

### Ingest events at any scale:

- No provisioning, partitioning, or load isolation worries.
- Expand with global topics.
- Enrich, deduplicate, order, aggregate, and land events using Cloud Dataflow.
- Durable storage.

### Simple development of event-driven microservices.

- Reliable delivery of each event to the services that must reaact to it.
- Push subs deliver the event to serverless apps.
- Pull subs make events available to more complex stateful services.
- Multi-region environments operate seamlessly.

### Be production ready from day one.

- ENd-to-end encryption, IAM, and audit logging.
- NoOps, fully automated scaling and provisioning.
- Extreme data durability and availability.
- Native client libraries and an open-service API.

## Cloud Pub/Sub is a middleware.

Is called middleware because it is positioned between applications.
It's used between data gathering and processing systems for example if an organizzation is hiring a new employee the company HR's syhstem can use cloud Pub/Sub to notify their other business systems that a new employee has been hired pass on relevant information and initiate actions. 
Cloud Pub/Sub is often found in the middle of systems like this.

HR System > Person-hired event "message" > HR "Topic" > Trigger employee directory service, badge activation, email account provisioning, etc.

## Cloud Pub/Sub uses the Publish-Subscribe pattern

Publisher applications can send messages to a topic and subscriber applications can subscribe to that topic to receive the message when the subscriber is ready, this can take place assynchronously, it's important to say that the subscriber only receive messaages form the initial publisher, it's best practice when using Cloud Pub/Sub with GCP tools to specify a subscription instead of a topic for reading.

Publisher > Message > (Cloud Pub/Sub - Topic (Message stored) send to -> Subscription) > Message > Sent to > Subscriber.

## Cloud Pub/Sub acts as a buffer across applications

Can be used to guarantee the email messages get delivered swiftly to online users as well as offline users when they come back online. Cloud Pub/Sub can act as a shock absorber within the architecture. 

If there's a sudden influx of messages cloud pub/sub avoids the risk of overwhelming the consumers of those message because it will absorb the sudden increase in messages and the consumers can continue to pull as many messages they can handle at once.

Messages can be pushed to any secure webserver or pulled from anywhere on the internet.


## Cloud Pub/Sub within the big data processing model

<img src="https://i.imgur.com/SAMf3iE.png">

- Ingest: Data is ingested through Cloud Pub/Sub subscriptions > Gets processed by Cloud Dataflow/Hadoop/Spark > Stored in the right place with the right permissions > Analyzed > Used in Data Warehouse, predictive analytics, catching and serving.

## Examples

- Every time your Gmail displays a new message is because of a push notification on your mobile device / pc.
- The updating of search resources as you type is a feed of real time indexing that depends of update caches with breaking news.
- Ads & Budgets.

<br>

# Lab Intro: Cloud Pub/Sub - Qwik Start - Python

Create a virtual environment for python3.

````
sudo apt-get update
sudo apt-get install virtualenv -y
virtualenv -p python3 venv
source venv/bin/activate
````

Install Pub/Sub client library & Clone the code.

````
pip install --upgrade google-cloud-pubsub
git clone https://github.com/googleapis/python-pubsub.git
cd python-pubsub/samples/snippets
````

## Pub/Sub - the Basics

Google Cloud Pub/Sub is an asynchronous global messaging service. There are three terms in Pub/Sub that appear often: topics, publishing, and subscribing.

A *topic* is a shared string that allows applications to connect with one another through a common thread.

*Publishers* push (or publish) a message to a Cloud Pub/Sub topic. Subscribers will then make a subscription to that thread, where they will either pull messages from the topic or configure webhooks for push subscriptions. Every subscriber must acknowledge each message within a configurable window of time.

In sum, a *publisher* creates and sends messages to a topic and a subscriber creates a subscription to a topic to receive messages from it.

## Pub/Sub in GCP. 

It comes preinstalled in the Cloud Shell, no installations required but with python we can create topic, subscriber and view messages. But to publish messages to the topic we will use Gcloud.

## Create a Topic.

````
export GLOBAL_CLOUD_PROJECT=qwiklabs-gcp-00-2c3a82cd09b9
````

````
python publisher.py -h
python publisher.py $GLOBAL_CLOUD_PROJECT create MyTopic
````

## List  Pub/Sub topics in given project.

````
python publisher.py $GLOBAL_CLOUD_PROJECT list
````

## Create a subscription

````
python subscriber.py $GLOBAL_CLOUD_PROJECT create MyTopic MySub
````

Log

````
Subscription created: name: "projects/qwiklabs-gcp-00-2c3a82cd09b9/subscriptions/MySub"
topic: "projects/qwiklabs-gcp-00-2c3a82cd09b9/topics/MyTopic"
push_config {
}
ack_deadline_seconds: 10
message_retention_duration {
  seconds: 604800
}
expiration_policy {
  ttl {
    seconds: 2678400
  }
}
````

Return subscribers for a given project:

````
python subscriber.py $GLOBAL_CLOUD_PROJECT list-in-project
````

## Publish messages

Now that you've set up MyTopic (the topic), a subscription to MyTopic (MySub), see if you can use gcloud commands to publish a message to MyTopic.

````
gcloud pubsub topics publish MyTopic --message "Hello"
````

## View messages.

````
python subscriber.py $GLOBAL_CLOUD_PROJECT receive MySub
````

Log

````
Listening for messages on projects/qwiklabs-gcp-00-2c3a82cd09b9/subscriptions/MySub..
Received Message {
  data: b"Publisher's name is <YOUR NAME>"
  ordering_key: ''
  attributes: {}
}.
Received Message {
  data: b'Hello'
  ordering_key: ''
  attributes: {}
}.
Received Message {
  data: b"Publisher's name is Jhan"
  ordering_key: ''
  attributes: {}
}.
Received Message {
  data: b'HEllo'
  ordering_key: ''
  attributes: {}
}.
````

Cloud Pub/Sub is not a messaging processing service. You write your applications to process the messages stored in Cloud Pub/Sub.

<br>

# Summary.

- APIs are software structures that present easy to understand interfaces and remove needless detail.
- Rest APIs ensure apps can communicate.
- There are a number of issues to consider as a part of the API design and development process.
- Cloud Endpoints is a distributed API management system that helps you create and maintain APIs.
- Apigee Edge is a platform for developing and managing API proxies.
- A Managed messaging system ingest, tranasforms and analyzes massive amounts of data. It also orchestrates complex business processes.
- Cloud Pub/Sub passes messages between data gathering and processing systems.