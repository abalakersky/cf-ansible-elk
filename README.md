# cf-ansible-elk
Step by Step



1. create a bucket to store files
2. Add bucket policy allowing access to files via HTTP and replace examplebucket with the name of your bucket:
       {
         "Version":"2012-10-17",
         "Statement":[
           {
             "Sid":"AddPerm",
             "Effect":"Allow",
             "Principal": "*",
             "Action":["s3:GetObject"],
             "Resource":["arn:aws:s3:::examplebucket/*"]
           }
         ]
       }
3. Upload the following files to the bucket
   1. AnsibleCreate.yaml
   2. ec2_create.yml
   3. elk_install.yml
   4. vaultp.txt this file needs to be created separately and must contain single line with password provided earlier
4. Initilize CloudFormation stack creation using URL address for AnsibleCreate.yaml
   1. Name the stack whatever you want
   2. Type in the http url of the bucket containing above files (do NOT type in the closing slash)
   3. Pick the default keypair to use for ansible server
   4. specify CIDR address for incoming SSH connections
   5. Continue to let the stack start.
