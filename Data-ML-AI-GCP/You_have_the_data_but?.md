# You have the data but how are you going to deal with it?

# Intro to Big Data managed services in the Cloud.

Enterprise stores system leaves the teraby behind to measure data size with petabyte becoming the norm.

1 Petabyte is 1kk Gigabites or 1,000 Terabytes.


## How big is a petabyte of data?

- A stack of floppy disks higher than 12 Empire State buildings to store 1 Petabyte.
- Download 1 Petabyte over a 4G network you will need 27 Years.
- 1 Petabyte of storage of every tweet ever tweeted multiplied * 50.

## How small is a petabyte of data?

- Only enough to store 2 micrograms of DNA.
- 1 day's worth of video uploaded to Youtube.

## Where big data comes in?

Every company saves data someway. 90% of data is unstructured, with all this data available companys are now trying to gain some insights into their business based on their data.

That's where BigData comes in. BigData analyzis the saved data to learn more about their services.

## Overview of big data managed services.

- Cloud DataProc: Process data with Hadoop/Spark.
- Cloud DataFlow: Analyze streaming data in real time.
- BigQuery: Modernize a data warehouse foundation. (SQL intop your data infrastructure.)

# Leverage Big Data Operations with Cloud Dataproc.

## Hadoop

Hadoop is a set of tool that enables a cluster to store and process large volumes of data and ties indevidual computers in a cluster.

## Spark.

Is an unified analytics engine for large scale data processing and achieves high performance for both batch and streaming data.

## CloudDataProc.

Creates clusters, manages it, and because they run ephemerally you can save cost $.

### Key features.

Cloud Dataproc is a managed service for batch, processing, querying and streaming and ML.

1. Virtual CPU/HR. (1c each) - Cost effective.
2. Are quit to start to scale and shutdown, fast and scalable.
3. Open source ecosystem (you can move spark and hadoop over there.)
4. Versioning (can move from image versions easily.)
5. Integration: Includes BigTable and ensures data will not be lost with the hand of Stackdriver as well.

## Typical Spark/Hadoop Clusters.

Obtain servers > Configure servers > Install OS > Configure OSS > Optimize OSS > Debug OSS > Process Data.
2
## Cloud Dataproc separates storage and compute.

Create cluster t+sec > Configure cluster (t+20sec) > Process data (t+90sec)

hdfs:// > gs:// (Changes the prefix and you can use Google Storage.)

## Hadoop and Spark Jobs and Workflows.

Cloud DataProc cluster:
- Spark and Hadoop open-source software > Cloud Dataproc agent > Cloud Services.

Cloud DataProc jobs:
- Spark> PySpark > SparkSQL > MapReduce > Pig > Hive.

Data outputs:
- Applications on the cluster > Cloud Dataproc jobs > GCP Products.

## Use cases

### Cloud Dataproc can help with Log processing.

#### The need:

Large volumes of data from several sources are aggregated and loaded into databases so metrics can be gathered for daily reporting, management, dashboards and analyzis.

A dedicated on-premises cluster ir currently used to store and process the logs with MapReduce.

#### The solution:

Cloud Storage provides a low-cost storage option.
An ephermeral Cloud DataProc cluster can be created in less than 2 mins. 

Data is processed with existing MapReduce.

#### The value

Saves money and reduces complexity.

### Cloud Dataproc can help with ad-hoc data analysis.

#### The need

In this organization analysts are using Spark Shell but are concerned about increase in usage.
Unsure on how to scale their cluster, which is running in standalone mode.

#### The solution 

Creates clusters that scale for speed and mitigate failure.

Can use web interfaces, Cloud SDK or native SPark Shell Via SSH.

#### The value

Unlocks the cloud without technical complexity.

Complex computations take seconds, not hours.

### Cloud Dataproc can help with machine learning.

#### The need

Spark Machine Learning Libraries (MLib) are used to run classification algorithms on large datasets.
There is reliance on cloud based machines to install and customize spark.

#### The solution

Spark and MLib can be installed on any Cloud Dataproc cluster.

Customizations can be applied to clusters via initialization actions.

Use stackdriver to monitor workflows. 

#### The value

Resources can be focused on data, not cluster creation and management.
Integration with GCP unlocks new Spark features.

# Dataproc: Qwik Start

Dataproc helps users process, transform and understand vast quantities of data.