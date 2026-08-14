# Google Cloud (GCP)

This folder contains notes about GCP services.


## GCP CLI

THe cloud system provides a CLI to interact with the cloud service.


gcloud auth list

## Compute region & zone

The compute zone is an approximate location in which your cloud resources live.
Each region has one or more zones. [Here](https://docs.cloud.google.com/compute/docs/regions-zones?hl=es) is the complete documentation about region and zones.

````bash
gcloud config set compute/region asia-south1
gcloud config set compute/zone asia-south1-a
#export a variable for REGION and ZONE!
````

