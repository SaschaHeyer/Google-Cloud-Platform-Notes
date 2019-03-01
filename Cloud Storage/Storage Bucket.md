# Google Cloud Storage Buckets

- Create buckets to store data
- Buckets are standalone (not required to have a instance running)
- Buckets are globally unique
  - Name (globally unique)
  - Location
  - Storage Class
- Data stored in a Bucket is called object
- Each object has a storage class 
  - can be changed for each object

## Bucket Storage Classes

### Multi-regional

* frequent access from anywhere in the world
* geo redundant (in at least two regions)
* used for (hot objects)
* 99,95 availablity sla

### Regional

* frequent access from a specific region
* can be used for storign data which is used in Compute Engine instances
* very similar to multi-regional

### Nearline

* accessed once a month at max
* 30 days minimum storage duration
* Higher per operation costs
* Data retreival costs
* ver low cost per GB storage
* can be used for backups, archival storage

### Coldline

* accessed once a year at max
* 90 days minimum storage duration
* similar to nearline
* infrequently accessed data, data for example stored for legal reasons



## Usage

* API
* gsutil
* Console
* Client Libraries (Java, Node.js, ...)

## Domain named Buckets

* Buckets can be domain named
* must be valid DNS names 
* Ends with an top-level domain
* Domain ownership verification is required

## Permissions 

* Permissions are possible for Buckets and for objects as well
* Groups, users or roles

## Lifecycle management

https://cloud.google.com/storage/docs/managing-lifecycles

* Specify how long files are stored before specific activities are triggered
* For example 
  * delete all files which are 30 days old

## Transfer Service

* Helps to get data into Cloud Storage
* Imports are possible from:
  * AWS S3 bucket
  * HTTP/HTTPS location
  * From local files
  * Between Cloud Storage Buckets
* It is possibel to set up recurring transfers
* Delete from destination if they do not exist in source
* Delete from source after copy
* Periodic synchronization



## Encryption

TODO