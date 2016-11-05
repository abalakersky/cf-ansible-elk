# cf-ansible-elk

This repository contains required CloudFormation and Ansible scripts to create a single instance in a VPC, install Ansible on that instance, then run Ansible Playbooks to create a second instance and install ELK on it.

### Step by Step instructions

1. create a bucket to store files
2. Add bucket policy allowing access to files via HTTP and replace the word `examplebucket` with the name of your bucket:
```
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
```
3. Upload the following files to the bucket
   1. AnsibleCreate.yaml
   2. ec2_create.yml
   3. elk_install.yml
   4. vaultp.txt `You will need to add to this file a single line containing password provided separately`
4. Initilize CloudFormation stack creation using URL address for AnsibleCreate.yaml
   1. Name the stack whatever you want
   2. Type in the http url of the bucket containing above files (do NOT type in the closing slash)
   3. Pick the default keypair to use for ansible server
   4. specify CIDR address for incoming SSH connections
   5. Continue to let the stack start.

## Results

After about 15-20 minutes you will find 2 instances in your AWS account. One named AnsibleELK-ansible, and the other elkserver. By accessing elkserver on its public IP with port 5601 you will be get to Kibana. Port 9200 will get you to Elasticsearch.
