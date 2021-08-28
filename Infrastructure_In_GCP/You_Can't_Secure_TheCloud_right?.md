# Introduction to Security in The Cloud

- Google has operated securelity in the cloud +20 years.
- 7 services have +1 billion users a day.
- Google connects to more than a billion IPs every day.

Countless organizations has lost data due to security incidents, can cost millions and lost business and can permanently damage as lost of customer trust.

## Leverage Google's technical infrastructure.

- Deployment of services.
- Storage of data.
- Communication between services.
- Operations by administrators.

## Google's infrastructure security layers.

> Hardware infrastructure: 
- State-of-the-art data centers.
- Security of physical premises.
- Hardware design and provenance.
- Secure boot stack and machine identity through cryptographic signatures.

> Service deployment:
- Service identity, integrity and isolation and inter-service access management. RPC is a way to facilitate communication between two services like REST over HTTP or XML by SOAP
- Encryption of inter-service communication.
- External bug bounty program.

Storage services > Internet communications > Operational security

# Undestanding the Shared Security Model.

When you build and deploy application in your on-premise infra you are the responsible for the security of the entire stack, from the physical hardware and that premises that are housed all the way to the encrypted data in disks, and network and all the way to the content stored in the applications.

But when you move your application to Cloud Google's handles many of those lower level of security like physical security, disk encryption and network integrity. The upper layers of the security stack includes securing data remains your responsability.

Gcloud provides the tools like the resource herarchy and Cloud IAM to find and implement policies but this is our responsability.

Data access is almost always your responsability.

# Explore Encryption Options.

There are several Encryption options on Gcloud.

- Encryption by default (Only on GCP)
- Customer-managed encryption keys.
- Customer-supplied encryption keys. (CSEK) this is often called client-side encryption.

## Server-syde encryption.

By default GCP will encrypt data in transit and in rest.
Data in transit is encrypted by TLS and in REST is encrypted with AES-256 key. 

The encryption happens automatically.

## Customer-managed encryption keys (CMEK)

You manage your own encryption keys that protect data on Google Cloud.

Cloud KMS automates and simplifies the generation and management of encryption keys. Keys are managed by the customer (you) but the key never leaves Google Cloud.
- Manage keys in a cloud-hosted solutions.
- Encrypt and decrypt via API.
- Automated and at-will key rotation.
- Symmetric and asymmetric key support.

## Customer-supplied encryption keys (CSEK)

- Use your own AES-256 encryption keys with GCP services.
- Store the keys locally and provide them as part of GCP api calls.
- GCP uses the key in-memory and it's inmediately discarded after use.

## Persistent disk encryption with CESK

- Data is encrypted before it leaves your instance.
- System defined or customer supplied keys.
- The deletion process renders data irrecoverable.

## Other persistent disk encryptions options.

- You can create your own persistent disks and redundantely encrypt them. 
- With client-side encryption is always an option, you will encrypt data before sending that to Google Cloud, your decryption keys never leaves your local devices.

# Understand authentication and authorization with Cloud IAM.

Cloud Identity and Access Management (IAM) enables administrators authorize `who` can `do_what` on `which_resource`.

IAM policies can apply to many types of users like resources. The WHO can be:

- Google account or Cloud Identity User.
- Service account.
- Google groups.
- Cloud Identity or G Suite Domain.

## How to manage GCP users.

Gmail Accounts and Google Groups.

Many users get started by logging to GCP with personal gmail account. To collaborate with their team mates they use Google Groups to gather together people who are on the same role.

But the teams are centrally managed, if someone leaves there is no way to remove him inmediately, somethings is better when you use Gsuite, because you can use groups to inmediately remove users with Admin console on GCP.

GCP users who are not Gsuite can gain the same capabilities through Cloud Identity. 

Cloud Identity allows users and groups to be managed using the GCLoud Admin Console but Gmail, docs, calendar aren't included.

## Cloud Directory Sync.

Microsoft Active Directory or LDAP > Google Cloud Directory Sync > Users and groups in the Cloud Identity Domain. (Scheduled one-way sync)

## Cloud Identity.

Unified identity access and device management platform.
- Is an Identity as a Service solution (IDaaS).
- Used for managing users, groups, and domain-wide security settings from a central location.
- Tied to a unique DNS domain that is enabled for receiving messages.

## IAM roles.

(The can do what part) is defined by an IAM role, that is a collection of IAM permissions. permissions are low-level and fined-grained.

For example, to manage a VM you need permissions to Create, Delete, Stop, Start and Change and instance. Permissions are usually grouped into a role to make things easier.

## Roles on specific items in the hierarchy.

(On which resource) when you gave a user group or sa permission on an specific element of the resource herarchy the resulting policy applies to the element you choose as well as the elements belows that resource in that herarchy.

### There are three types of IAM roles in GCP.

*Primitive:* Applies across all GCP resources in a Project, that includes Owner > Editor > Viewer and Billing Admin.
- Owner: Invite members, remove members, Delete projects, + what an editor and viewer can do.
- Editor: Deploy applications, modify code, configure services, + what a viewer can do. 
- Viewer: Read only access.
- Billing admin: Manage billing, add and remove administrators.

*Predefined:* Applies to a particular GCP service in a project. GCP services offer their own set of predefined roles and they defined where those roles can be applied. 
For example, GCE offers a set of predefined roles and you can apply them to compute engine resources in a given project, a folder or the entire organization. 
Another example is Cloud BigTable that is a managed database service, BigTable offers roles that can apply to aqn entire organization, to a particular project or even individual cloud bigtable database instances.

- IAM predefined roles offer more fine-grained permissions on particular services. The Google Compute engine InstanceAdmin role allows who ever has it to perform a certain set of actions in virtual machines.

Example: A google group that has InstanceAdmin role in project_a.

*Custom:* For some organizations the primitive and predefined IAM roles may not offer enough granularity. This one let's you create your own roles with very granular permissions.

Example: We defined an InstanceOperator role that just provides access to get/list/start/stop instances but don't give permission to delete them or modifiy VM's.

Custom roles can only be applied to projects and organizations, can't be done in Folders.

## Service accounts

COntrols service to service communications.
- You must provide an identity.
- Used to authenticate from one service to another.
- Used to control privileges.

Example: You have an application running in a virtual machine that needs to access data in GCS, you only want that VM to access that data, you can create a Serviceaccount that is authorized to access that data in GCS and attach that serviceAccount to the virtual machine.

- Identified with an email address account.

Example: 
- PROJECT_NUMBER-compute@developer.gserviceaccount.com
- project_id@appspot.gserviceaccount.com

## Service accounts and IAM.

Identity (Service Account) > Has an IAM role (InstanceAdmin role) > Resource (Compute Instances).

Serviceaccounts needs to be managed too. Fortunately we can modified them as a resource and can have IAM policies attached to them so one person can have editor role on that serviceaccount and other one can have viewer role.

## Managing VM permissions.

You can grant virtual machines different identities.
You can manage permissions of serviceaccounts without having to re-create the virtual machine.

## Grant different identities to diferent groups of VM's.

<img src="https://i.imgur.com/yJ0myIs.png">

# User Authentication: Identity-Aware-Proxy (Cloud IAP).

Is a resource that can be used to implement authentication to HTTPs based applications without the use of VPNs. 

Cloud IAP let's you stablish a central authorization layer to applications over TLS so you can use application level access control instead of relying on Network level firewalls.

Applications and resources protected by IAP can be only accessed by the Proxy with Users/Groups with the correct Cloud IAM role. The proxy provides a layer of protections between the outside world and your internal service.

When you grant a user access to an application/resource by cloud IAP their are subject to the fine-grained access control implemented by the product in use without the requirement of use a VPN. Cloud IAP performs authorizations and authentications when an user wants to access to an IAP secured resource.

Cloud IAP secures authentication and authorizations of external requests by a TLS. Cloud IAP doesn't protects against activity inside of your VM like if someone has access to the VM by SSH.

Cloud IAP doesn't protect agains activity between a project like VM to VM communication between your project over the local network.

# IAP Lab.

Download the code and move to the folder.

````
git clone https://github.com/googlecodelabs/user-authentication-with-iap.git && cd user-authentication-with-iap
````

Deploy the app engine.

````
cd 1_HelloWorld
gcloud app deploy
````

Activate Identity-Awary-Proxy on Security > IAP.

Activate IAP as Internal User type and fill it with proper values. (The url is the AppEngine one.)

Disable flex api.

````
gcloud services disable appengineflex.googleapis.com
````

Access User Identity Information
Once an app is protected with IAP, it can use the identity information that IAP provides in the web request headers it passes through. In this step, the application will get the logged-in user's email address and a persistent unique user ID assigned by the Google Identity Service to that user. That data will be displayed to the user in the welcome page.

````
cd ~/user-authentication-with-iap/2-HelloUser
````

Deploy again.

Turn off IAP
What happens to this app if IAP is disabled, or somehow bypassed (such as by other applications running in your same cloud project)? Turn off IAP to see.

In the cloud console window, click Navigation menu > Security > Identity-Aware Proxy. Click the IAP toggle switch next to App Engine app to turn IAP off.

Since the application is now unprotected, a user could send a web request that appeared to have passed through IAP. For example, you can run the following curl command from the Cloud Shell to do that (replace <your-url-here> with the correct URL for your app):

````
curl -X GET <your-url-here> -H "X-Goog-Authenticated-User-Email: totally fake email"
````

# Identifying Best Practices for Authorization using Cloud IAM.

- Use projects to group resources.
- Check the policy granted on each resourec.
- Use principle of least privilege.
- Use logs.
- Audit membership.

## Service accounts best practices.

- Exercise care granting the serviceAccountUser role.
- Provide a display name that clearly identifies its purpose.
- Establish a naming convenction.
- Establish key rotation policies and methods.

# Quiz

check
1.

Which of the following is not an encryption option for Google Cloud?
check
Scripted encryption keys (SEK)

Google encryption by default

Customer-managed encryption keys (CMEK)

Customer-supplied encryption Keys (CSEK)
Scripted encryption keys is not an option with Google Cloud.

check
2.

If a Cloud IAM policy gives you Owner permissions at the project level, your access to a resource in the project may be restricted by a more restrictive policy on that resource.
check
False

Policies are a union of the parent and the resource. If a parent policy is less restrictive, it overrides a more restrictive resource policy.

check
3.

check
User identities are created outside of Google Cloud using a Google-administered domain

# Summary.

- Security is the heart of all GCP use and development.
- Security responsabilities are shared between Google infrastructure and the customer (data).
- There are four different encryptions options available: GCP default encryption, CMEK, CSEK and client-side encryption.
- Cloud IAM controls who can take actions on resources.
- Cloud IAP lets customers enforce access control policies for applications and resources.
- Best Practices for authorization using Cloud IAM include leveraging resource hierarchy, groups and service accounts effectively.