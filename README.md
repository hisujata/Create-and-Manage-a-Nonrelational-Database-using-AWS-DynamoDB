Create and Manage a Nonrelational Database using AWS DynamoDB

DynamoDB is a NoSQL database, allowing for flexible schema design that can evolve with your application. It provides low-latency performance with near-infinite scaling, so you do not need to worry about performance bottlenecks as your application grows. Create DynamoDB tables with required secondary keys and perform CRUD operations. Use Python and Boto 3, AWS SDK for Python, for ineracting with the DynamoDB APIs.

#DynamoDB, #NoSQL, #Python, #Boto3, #EC2

Step 1: EC2 instance configuration

#a. DynamoDB IaaS Setup

1) Create an Amazon Linux 2 EC2 instance with ports open for port numbers 22 and 8000
2) Attach the role created above to the instance
3) SSH into the instance using your preferred SSH client
4) Run the below commands into the terminal once the SSH connection is successful

sudo yum update

sudo yum install python-pip -y

sudo yum install awscli -y

pip install boto3

sudo yum install java-1.8.0-openjdk

mkdir dynamodb-local

cd dynamodb-local

wget http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest.tar.gz

tar xzf dynamodb_local_latest.tar.gz

java -Djava.library.path=./DynamoDBLocal_lib/ -jar DynamoDBLocal.jar &

5) Keep this terminal window open for the rest of the exercise. If the program crashes or you get logged out of the instance, restart the program. Use a new terminal window for the rest of this exercise. 

<img src="https://github.com/hisujata/Create-and-Manage-a-Nonrelational-Database-using-AWS-DynamoDB/blob/master/screenshot1.png">

<img src="https://github.com/hisujata/Create-and-Manage-a-Nonrelational-Database-using-AWS-DynamoDB/blob/master/Screenshot2.png">

Step 2: CRUD operations on local DynamoDB deployment

#b. Deployment of Python Script

1) Download the script dynamo-ops2.py
2) Use your preferred SCP client to copy it to the folder /home/ec2-user in the instance created above
3) SSH into the instance again
4) Run the following command in the terminal to execute the python script
python dynamo-ops2.py
5) Run the below commands  to verify that the table has been created

● aws configure
Skip the access key and secret access key fields. Enter the region as us-east-1 and format as json

● aws dynamodb list-tables --endpoint-url http://localhost:8000

<img src="https://github.com/hisujata/Create-and-Manage-a-Nonrelational-Database-using-AWS-DynamoDB/blob/master/Screenshot3.png">

<img src="https://github.com/hisujata/Create-and-Manage-a-Nonrelational-Database-using-AWS-DynamoDB/blob/master/Screenshot4.png">

<img src="https://github.com/hisujata/Create-and-Manage-a-Nonrelational-Database-using-AWS-DynamoDB/blob/master/Screenshot5.png">

Step 3: Creation of DynamoDB table with secondary index. 

#c. Deployment of Python Script 

1) Create another EC2 instance and configure it as shown in Step 1. Also, configure the AWS CLI as shown in Step 2.
2) Download the provided script dynamo-advanced.py. 
3)  Use your preferred SCP client to copy the given script dynamo-advanced.py to the EC2 instance created above into the location /home/ec2-user
4) SSH into the EC2 instance again
5) Run the provided Python program using the command below
python dynamo-advanced.py
6) Verify the table creation is successful using the following command
aws dynamodb list-tables --endpoint-url http://localhost:8000
7) Show the properties of the table using the command below
aws dynamodb describe-table --table-name orders --endpoint-url http://localhost:8000


Cloud is always pay per use model and all resources/services that we consume are chargeable. After completing the project, make sure to delete each resource created in reverse chronological order if you do not wish to use the resources.


