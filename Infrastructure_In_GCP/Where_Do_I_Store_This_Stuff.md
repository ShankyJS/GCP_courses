# Storage options in the cloud.

All applications create an utilizes data.

Cloud Storage -> Applications needs storage to manage and operate resources.
For relational databases we use CloudSQL and CloudSpanner.

For No-relational we use CLoud Datastore and BigTable.
BigQuery is a highly scalable data warehouse and falls out of this storage modules.

## Three Common uses for GCS

1. Content storage and delivery (content fast running on the global network for users).
2. Storage for data analytics and general compute.
3. Backup and archival storage.

## Two priorities for databases users.

Migrate existing databases to the cloud and move them to the right service.
Innovate, build or rebuild for the cloud, take advantage of mobile and plan for future growth.

# Structured and Unstructured Storage in the Cloud.

1. Structured is what most peoples uses, and usually fits within columns and rows or spreadshets in relational databases.

Examples like; names, lastnames, addresses, contact numbers and billing info.

The benefit is that can be undestructured by programming languages and data can be manipulated relative quickly.

It's estimated that 80% is unstructured data. It's far more difficult to process this kind of data when you use traditional methods, 

Often includes text and multi-media content like photos, videos, webpages, so on. 

Organizations in mining unstructured data for insights that will promote with the competition.

Flow chart to select which is the best storage type for me.

<img src="https://i.imgur.com/UWrcyUI.png">

## Unstructured Storage using Cloud Storage.

Cloud Storage is just one of the many storage options in GCP, stores object data also known as blobs.

You can store unlimited amount of objects and up to 5TB in size each. gcs is well suited for binary or object data such as images, media servings and backups.

CloudStorage is the same storage that Google uses in Google Photos, Docs, gmail attachments and so on. 

Users cases multiple use cases.

Cloud Storage offers classes based on user's use case.

### Classes

GCS Classes are based on how often the user access the data.

- Multi-regional: Geo-redundant storage. (Costs a bit more GCS but you can a broad geographical location like USA, EU, or Asia and GCS stores your data in at least two geogrpahic locations separated by at least 160 kilometres this options is ideal for storing data that is frequently access like streaming videos, gaming mobile applications, websites.)
- Regional: Let's store your data in specific GCP region like us-central-1, it's cheaper than multi-regional but doesn't have redundancy this option is ideal for data analytics and machine learning. Local access to compute resources will increase a lot the performance.
- Nearline: Data accessed less than once a month, is a low cost highly durable storage service for infrequently accessed data, this choice is better than regional/multi when you plan to read or modify your data on average once a month or less. For example if you want to continously add files to GCS and plan to access it once a month, this is a nice option. This usually is online-backups, sourcefile storage, etc.
- Coldline: Data accessed less than once a year, is a very low cost highly durable storage service for data archiving online backups and data recovery the best option for data that you plan to access almost once a year, due to this slighly lower availability 90-day minimum storage duration cost for data access and higher pre operational cost. Usually used for archive data, with lengthy storage durations from legal or regulatory requirements, tape migrations and disaster recovery.
It has a single API and milliseconds data access latency and 11 ninth durability across all storage classes. 

GCS also offers object lifecycle management that automatically move data to lower cost storage classes as it is accessed less frequently throughout its life.

## Cloud Storage organizes files into buckets

When you create a bucket you give it the following details:
- Globally unique name.
- Location (region or multi-region).
- Default storage class.
- IAM policies or access-control lists.
- You can access ACL's defining which levels of access people have and it has scope and permission (which action can uses)
- Object versioning setting. (This works a lot with terraform)
- Object lifecycle management rules. (You can say that GCP deletes files when they are 365+ for instance.)

# Starting with GCS Lab.

Download image.

````
wget --output-document ada.jpg https://upload.wikimedia.org/wikipedia/commons/thumb/a/a4/Ada_Lovelace_portrait.jpg/800px-Ada_Lovelace_portrait.jpg
````

Upload the image to the bucket.

````
gsutil cp ada.jpg gs://my-new-bucket-312314
````

RM from your local and download it from the bucket.

````
rm ada.jpg
gsutil cp -r gs://my-new-bucket-312314/ada.jpg .
````

Copy an object to a folder in the bucket

````
gsutil cp gs://my-new-bucket-312314/ada.jpg gs://my-new-bucket-312314/image-folder/
````

Make it public

````
gsutil acl ch -u AllUsers:R gs://my-new-bucket-312314/ada.jpg
Updated ACL on gs://my-new-bucket-312314/ada.jpg
````

Remove public:

````
gsutil acl ch -d AllUsers:R gs://my-new-bucket-312314/ada.jpg
No changes to gs://my-new-bucket-312314/ada.jpg
````

# SQL Managed Services

A Database is a collection of informatio nthat is organized so that it can be easily be accessed and managed.

Computer applications runs applications to get fast answers to questions like:

- What's this user's name given their sign-in information so I can display it?
- What's the cost of product Y so I can show it on my dynamic webpage.
- What were my top 10 best selling products this month?
- What is the next ad I should show the user currently browsing my site.

Apps need to write/read data.

## Relational Databases are most common.

Relational Database management systems.

- RDBMS
- relational databases.
- SQL Databases.

Suitable use cases:

- Have a well structured data model.
- Need transactions.
- Ability to join data across tables to retrieve complex data combinations.

GCP offers two SQL-based management services.

### CloudSQL:
Managed MySQL or Postgresql Database. When setting up CloudSQL with replicas that's automated. The infrastructure is managed,
That includes; backups, updates, failovers and maintanence. 

The database can:

- Automatic replication.
- Managed backups.
- Vertical scalling (read and write)
- Horizontal scaling (read)

### Cloud Spanner:

CloudSpanner is an strongly consistent horizontal scalable managed relational database. 
This service can runs across multiple nodes, either in a single region or to multiple regions.

The managed service automatically replicates data to the nodes.

Is compliant with ANSI 2011 With extensions


# Exploring CloudSQL.

Make it's easy to mantain manage and administer relational mysql and postgres dbs in the cloud, it allows you to focus in your applications, it's perfect for:

- Wordpress sites,
- E-commerce.
- Geospacial applications.
- CRM's.

It's fully managed, not requires software installation and automated backups, replication, patches and updates greater than 99.95% availability everywhere in the world.

## Performance and scalability 

- Scales up to 64 processor cores and 400+ GB of ram
- Maximum of 10 TB of storage.

## Reliability and security.

- High availability with automatic failovers.
- Easiliy configure replication and backups.
- Data is encrypted.

## Compatibility

- Accessible from almost any app.
- Easy to move and migrate data.

It's also provides migration tools like MySQL workbench with standarized migration languages.

# Cloud SQL for MySQL (Lab)

Create db manually and store password ``pe2Jyn96gO9DM0qO``

Connect to the db

````
gcloud sql connect myinstance --user=root
````

Create a db

````
create database guestbook;
USE guestbook;
CREATE TABLE entries (guestName VARCHAR(255), content VARCHAR(255),
    entryID INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(entryID));
    INSERT INTO entries (guestName, content) values ("first guest", "I got here!");
INSERT INTO entries (guestName, content) values ("second guest", "Me too!");
````

And select the data.

````
select * from entries;

+--------------+-------------+---------+
| guestName    | content     | entryID |
+--------------+-------------+---------+
| first guest  | I got here! |       1 |
| second guest | Me too!     |       2 |
+--------------+-------------+---------+
````

# Cloud Spanner as a Managed Service

The difference is that Cloud Spanner combines the benefits of relational databases with non-relational horizontal scale.

Vertical scale is were you make your instance larger or smaller in resources.
Horizontal scale is when you scale by adding or removing servers or nodes. This makes Spanner uniques.

## Cloud Spanner vs other databases.

1. Familiar relational database structure.
2. Scales to very large databases.
3. Strong external consitency. (Data added is inmediately available)
4. Reduces operational overheads to keep data only and with traffic.

## Cloud Spanner features.

### Scale + SQL
- Scales horizontally.
- Low latency, transactional consistency, and high availability. (5 MINUTES A YEAR OF MAINTENANCE)
- Future-proofs database backends.

### Fully Managed
- Create or scale a globally replicated database in a few clicks.
- Synchronous replication and maintenance built in.

### Launch faster.
- Relational semantics.
- ACID transactions.
- Schemas.

### Enterprise grade security.

- Data-layer encryption in transit and in REST.
- IAM integration.
- Audit logging.

## How Cloud Spanner works?

Synchronous replication across multiple regions and zones, if one region goes off you can still access your data from another regions.

# Options for NoSQL based managed services.

1. Cloud Datastore: Fully managed serverless NoSQL that supports assets transactions.
2. Cloud BigTable: Petabyte scale sparse wide column no sequel database that offers extremely low latencies. 

# Cloud Datastore a NoSQL Document Store.

Cloud Datastore is a highly scalable noSQL database ideal for rapid and flexible web and mobile development, is schemaless. 
Cloud Datastore is there for ideal if you have no relational data and want to serverless databases without having to worry about Infrastructure.

Is the default solution for data being used for analyzis.

## Features.

### Schema-less.
- Change your data structure as your app evolves.

### Fast and highly scalable.
- High-speed queries no matter the size  of the database.
- Seamless scaling.
- Uses GQL Google Query Language.
- Built-in Cloud Datastore and composites indexes.

### Fully managed.
- Instantly provision an scalable and available NoSQL database.
- Automatic sharding and replication.

### Integrated and secure.
- RESTful interface makes data accessible by any deployment target.
- Serves as an integration point.

## Use cases:

1. User game profiles.
2. Product catalogues (Data herarchy can be strongly grouped together.)
3. Recording transactions based in asset properties. (Transfer founds from a bank to another).
4. Mobile games: Provides a durable key value store that allows data efficiently stored and access.

# Cloud Bigtable as a NoSQL Optional.

Aligns with no-relational database requirements. And it's made for large analytical and throughput intenses operational workloads. Great for user analytics, IoT, Financial data analyzis, graph data.

Cloud Bigtable is the one that powers: 

- Google analytics
- Google Searcher.
- Google maps.
- Gmail.

(Access to petabytes of Data.)

## Features

### Fast and performant.
- High performance under high loads.
- Faster, more reliable, and more efficient.
- Low latency.

### Seamless scaling and replication.
- Billions of rows and thousands of columns.
- No downtime during reconfigurations.
- Replication adds high availability.

### Fully managed.
- Database configruation and tuning handled by Google.
- Data backups created for disaster recovery.

### Integrated and secure.
- Integrated with open-source big data tools for powerful data analysis.

## Cloud Bigtable Interaction.

Can by read from managed vm's, javaservers, and almost whatever.

Data can be streamed with processing frameworks like Cloud Dataflow, storm, etc.

If streaming is not an option can be read by Batch processing by Spark, Cloud Dataflow.

### Cloud Bigtable Structure.

<img src="https://i.imgur.com/eFFMxCO.png">

Storage is in colossus that is google file system in Tablets. 
IT has inmutable maps where key values are bits.

Every single of node you add you can see that queries per second are larger.

# Summary

- Thre are three common uses for GCS: content storage and delivery, storage for data analytics and backup and archival storage.
- GCS is suited to the storage of unstructured data.
- There are thre classes of Cloud Storage(Regional, multi-regional, nearline, coldline).
- CLoudSQL is fully managed, relational database.
- CloudSpanner combines the benefits of relational database strucutre with non-relational horizontal scale.
- Cloud Datastore is ideal for highly scalabel NOSQL database.
- CloudBigtable aligns with NoSQL requirements and it's high performance service for large analytical and throughpout intensive operational workloads.