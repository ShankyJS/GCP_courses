# Learning objectives:

Describe the different ways a user can interact with the Google Cloud Platform (GCP).

- Discuss how to navigate the GCP env with GCP console.
- Explain the purpose and process of creating GCP Projects.
- Explain how billing works in GCP.
- Detail how to install and set up the CloudSDK

# The GCP console.

There are four ways to interact with GCP. 

- GCP console (that provides a Web UI).

Centralized console for all project data.
Execute common tasks using simple mouse clicks, preventing type errors.
Manage and Create projects (All resources has to be created in a logical project).

For ex. You might start a project and want some just users to access that resources, while all team members can access resources in a different project.

GCP console is great for developers because Access to Developer Tools:

- CloudSDK and CloudShell (provides command line interface).


Cloud Source repositorios, Cloud SDK (set of command line tools in GCP), CloudShell (gives you a shell without having to download with anything).

- Rest Based Apis (For custom applications)
- Cloud Console Mobile App for IOS and Android.

# Understanding Projects.

All resources must belong to a GCP project.

Projects are the bases for enabling and using GCP services like managing APIS, enabling billing, adding and removing collaborators and enabling other google services.

Each project is a different account and each resource belongs to exactly one.

Projects can have different owners and users.

## Resource manager.

Let's you programatically manage your projects in GCP, with the API you can interact with this Resource manager to create, remove, unremove projects.

## Projects

Projects have three identifying attributes.

1. Project ID: is a permanent unchangable identifier that has to be unique.
2. Project Name: Need not be unique, chosen by you, mutable. YOu can't use the name of a deleted project.
3. Project Number: GLobally unique, assigned by GCP, inmutable.


# How billing works

Billing in GCP is set up in the project level, when you define the project you have to select a billing account that has your payment option and all payment details.

A billing account is linked to a zero or more projects.

Accounts are charge automatically, invoice monthly or invoice at the threshold lmit.

Subaccounts can be used for separate billing for projects.

## How to keep your billing under control?

1. Budgets and Alerts.

You can define budgets at the billing account level or at the project level. You can define alerts for example if limit is 100 when there are 80 dollars billed you can get a notification.

You could trigger a script to shutdown things when billing exceeds the level.

2. Billing export.

Allows to store billing information in places that makes easy to retrieve to external analizis such as BigQuery or CloudStorage bucket.

3. Reports.

Let's you manage your expenses in a graphical way based on project or services

4. Quotas.

Limits unforseen extra billing charges quoates are created preventing overconsumption of resources because errors or malicious attacks.

There are two types.

Rate Quota: After specific times, for example GKE implements 1,000 to it's api from each GCB project every 100 seconds.

Allocation Quotas limites how many resources you can have in the region. Ex. 5 networks per project. 

You can change qoutas requesting to Google Cloud Support.

GCP quotas protects your billing from spikes of usage.


# Install and Configure CloudSDK

CloudSDK is a set of command tools that can be installed in your computer to use managed resources and applications in GCP.

Gcloud manages authentication, local configuration, developer workflow and interactions with the API.
Gsutil provides command line access to cloud storage objects and buckets.
Bq allows you to run query and manipulate datasets and entities in BigQuery through the command line.


## CloudShell provides an alternative to CloudSDK, because you don't need to install anything.

Runs on ephemeral Compute Engine VM at no cost to you.
No need to install CloudSDK or Other tools locally.
Browser based CLI access to the resources.
5 GB Of persistent disk storage.
Web preview functionality and buil-in authorization for project/resources access.


## Getting Started with CS and Gcloud

````
student_02_2dcaac0a47cc@cloudshell:~ (qwiklabs-gcp-01-fbfc4a5f620e)$ export ZONE=us-central1-a
student_02_2dcaac0a47cc@cloudshell:~ (qwiklabs-gcp-01-fbfc4a5f620e)$ echo $PROJECT_ID
qwiklabs-gcp-01-fbfc4a5f620e
student_02_2dcaac0a47cc@cloudshell:~ (qwiklabs-gcp-01-fbfc4a5f620e)$ echo $ZONE
us-central1-a
student_02_2dcaac0a47cc@cloudshell:~ (qwiklabs-gcp-01-fbfc4a5f620e)$ export ZONE=us-central1-a^C                                                                                                                                                  
student_02_2dcaac0a47cc@cloudshell:~ (qwiklabs-gcp-01-fbfc4a5f620e)$ gcloud compute instances create gcelab2 --machine-type n1-standard-2 --zone $ZONE
````

# GCP Apis.

Restful APIS are enabled through the GCP console.
Programmatic Access is provided to products and services.
- Code typically uses JSON as an interchange format..
- Use Oauth 2.0 for authentication and authorization.
- To help you control spend, most include daily quotas and rates (limits). Quoutas and rates can be raised by request.

Use client libraries to create a manage resources:

GCP -> CloudSDK > gcloud/bq/gsutil
GCP -> Cloud Client Libraries > Java/Rb/Go/Python/Go/NodeJS/PHP
GCP -> Restful API > Get/post/put/delete <- JSON

GOogle APIs Explorer help you to write your code.


# Summary:

The GCP console provides web based GUI for you to manage your GCP projects and resources.
All GCP services you use are associated with a project.
Your billing account pays for resources at a project level.
GCP also implements quotas, which limit unforeseen extra billing charges.
CloudSDK is a command-line interafce for GCP products and services.
CloudShell is an alternative to CloudSDK.
The services that make up GCP offer APIs so that code you write can control them.
The GCP console includes a tool called the APIs explorer.