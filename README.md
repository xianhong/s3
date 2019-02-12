## Interact with S3 compatible object storage with "s3curl.pl" script

### Step-1：Pull the docker image from docker hub
   docker pull yangxh/s3curl:new

### Step-2: Prepare a “.s3curl”file from a sample template in working directory. You only need to change access & secret keys and endpoints. Change ".s3curl" file ownership (ex: chown root:root .s3curl && chmod 600 .s3curl) 

### Step-3: (In your working directory,) Docker run a container from the image (yangxh/s3curl:new) to execute "s3curl.pl" script, the Perl wrapper of curl command, to interact with S3 compatible object storage. 

Examples: 
  * Create a bucket:
  docker run --rm -v $PWD:/home yangxh/s3curl:new -X PUT https://object.ecstestdrive.com/test_Bucket
  
  * Create object (Upload a file to an object)
  docker run --rm  -v $PWD:/home yangxh/s3curl:new -X PUT --data-binary @file https://object.ecstestdrive.com/test_Bucket/file
  
  * List objects in a bucket 
  docker run --rm -v $PWD:/home yangxh/s3curl:new https://object.ecstestdrive.com/test_Bucket
  
  * List different versions of objects in a bucket
  docker run --rm -v $PWD:/home yangxh/s3curl:new  https://object.ecstestdrive.com/MY_Bucket?versions
  
  * Download an object to a local file
  docker run --rm -v $PWD:/home yangxh/s3curl:new -o ECS.pptx https://object.ecstestdrive.com/MY_Bucket/ECS%20update.pptx

  * Create an object and set its retention time
  docker run --rm  -v $PWD:/home yangxh/s3curl:new -X PUT -H 'x-emc-retention-period:60' --data-binary @ECS.pptx https://object.ecstestdrive.com/test_Bucket/ECS.pptx

  * Delete an object
  docker run --rm -v $PWD:/home yangxh/s3curl:new -X DELETE  https://object.ecstestdrive.com/test_Bucket/ECS.pptx




  
