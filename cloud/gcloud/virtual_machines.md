## Virtual machines creation

Virtual machines can be deployed using the Google cloud console or using the gcloud CLI.

````bash
gcloud compute instances create gcelab2 --machine-type e2-medium --zone=$ZONE

gcloud compute ssh gcelab2 --zone=$ZONE
````

## Persistent Disk

