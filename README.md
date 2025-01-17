# Reply_task

### 1. Export from DynamoDB to JSON

1.	Selected technical-interview table in DynamoDB
2.	Select Export and Stream option and set up an export to an S3 bucket using DynamoDB Export to Amazon S3.
3.	Create a new bucket in S3 and mentioned this as destination S3 bucket ‘s3://dynamodbdataload/tabledata’
4.	Turned on PITR for 5 days and exported the data in JSON format
### 1. Export from DynamoDB to CSV
	
1.	As exporting a DynamoDB table directly to CSV using the AWS Management Console is not a built-in feature of DynamoDB, I used lambda function to export to csv
2.	Create a lambda function and a new role with basic Lambda permissions, inline policy to access dynamodb and s3 is created.
3.	As I can’t access data.csv from tmp folder, as it’s session specific, downloading the csv file to newly created s3 bukcet 
4.	Deploy the code, save and run the test 
5.	Now the results are saved to s3 bucket 
### 2. RDS

1.	Created Bastian Host in Public subnet in the same VPC as the RDS instance. 
2.	Configured Bastian host security group to allow SSH access 
3.	Configured RDS instance security group to allow inbound traffic on the database port (3306 for MySQL) from the security group of the EC2 instance.
4.	Connect to the EC2 instance in 
5.	Connect to RDS instance from the Bastian host using its endpoint and the credentials provided in AWS Secrets Manager

### 3. DB Connections

1.	After accessing RDS database ‘LakshmiRevanur’, listed the tables and none is seen
2.	A new table is created
3.	Created IAM role ‘EC2S3AccessRole’ for EC2 instance to access csv file in the s3 bucket
4.	Attach that role to EC2 instance
5.	Modify S3 bucket policy to allow ‘EC2S3AccessRole’
6.	Using S3 copy command, the file in S3 bucket is copied to the tmp folder of instance connect session.
7.	From AWS CLI, the csv data is loaded into RDS database table using query LOAD DATA LOCAL INFILE.

### 4. OpenSearch

1.	Created an EC2 instance with ssh inbound rules and all traffic outbound rule
2.	Installed nginx on the Ec2 instance and configured it and added VPC endpoint
3.	Start nginx service 
4.	Modify Security Group of OpenSearch instance to allow https from nginx server
5.	Modify Security Group of the Ec2 instance to allow http from my IP address
6.	OpenSearch dashboard is now accessible
7.	Created a new index in Stack Management -> Index patterns -> Create index pattern, that matches the field format of the data in exported files from Dynamo DB
8.	Added data into the created index using POST command in Dev Tools Console in OpenSearch UI.

But I am yet to find out a way to import data from the JSON files and load into the index. As I have committed to send by now, so sharing the task steps till here. 


### 5. EKS

1. Initially I faced Kubernetes RBAC issue and I was not able to access EKS cluster via kubectl. 
2. IAM user/role is listed in the aws-auth ConfigMap under the mapRoles/mapUsers section in the template file in CloudFormation. I modified the template by adding the user and created a new stack from it, where I am able to access pods, nods etc.

But I am yet to work on deploying the container. 

### 6. Generic AWS
I have to work on this yet and needed some more time. 











