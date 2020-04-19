## Interact with S3 compatible storage with AWS CLI
### Step-1: Install AWS CLI (Python version >= 2.7)
 `pip install –upgrade –user awscli`
### Step-2: Create `config` & `credentials` files in `$HOME/.aws` folder
   `mkdir $HOME/.aws`<br/>
   `config` file example:<br/>
  ```
     [ecs]
     output=json
 ``` 
  `credentials` file example:<br/>
 ``` 
    [ecs]
    aws_access_key_id = <YOUR_ACCESS_KEY_TO_STORAGE>
    aws_secret_access_key = <YOUR_SECRET_ACCESS_KEY_TO_STORAGE>
 ``` 
### Step-3: AWS CLI commands examples
* Create a S3 bucket named `bucket2`
```
aws --profile ecs --endpoint-url=http://<STORAGE_IP>:<PORT> s3api create-bucket --bucket bucket2
aws --profile ecs --no-verify-ssl --endpoint-url=https://<STORAGE_IP>:<PORT> s3api create-bucket --bucket bucket2
```
* Sync contents from bucket `MY_Bucket` to bucket `bucket2`
``` 
aws --profile ecs --endpoint-url=http://<STORAGE_IP>:<PORT> s3  sync s3://MY_Bucket s3://bucket2
aws --profile ecs --no-verify-ssl --endpoint-url=https://<STORAGE_IP>:<PORT> s3  sync s3://MY_Bucket s3://bucket2
```
* List bucket `bucket2`
```
aws --profile ecs --endpoint-url=http://<STORAGE_IP>:<PORT> s3  ls s3://bucket2
aws --profile ecs --no-verify-ssl --endpoint-url=https://<STORAGE_IP>:<PORT> s3  ls s3://bucket2
```
## (Folder: s3curl) Interact with S3 compatible object storage with "s3curl.pl" script

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




  
