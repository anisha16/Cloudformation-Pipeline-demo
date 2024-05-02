# Cloudformation-Pipeline-demo

**Problem Statement:**
A Jenkins pipeline has been implemented to automate the process of creating CloudFormation stacks, which in turn deploy S3 buckets and create SNS topics. 

**Continuous Integration (CI)**: This is the practice of frequently integrating code changes into a shared repository. Each integration triggers an automated build and test process to validate the changes. 

**Continuous Delivery (CD)**: This extends CI by automating the deployment process so that every validated change to the codebase can be reliably deployed to production or production-like environments. 

**Pipeline**: The CI/CD pipeline is a sequence of automated steps or stages that code changes go through, from version control to deployment. Each stage in the pipeline performs specific tasks such as compiling code, running tests, building artifacts, and deploying applications. The pipeline ensures that code changes are automatically validated and promoted through various environments (e.g., development, staging, production) before reaching end-users.

**CloudFormation**: CloudFormation is a service provided by Amazon Web Services (AWS) that allows us to define and deploy infrastructure as code. By defining infrastructure in CloudFormation templates, we can achieve repeatability, scalability, and efficiency in deploying and managing their cloud resources. 

**SNS Topics** : SNS (Simple Notification Service) is a fully managed messaging service provided by Amazon Web Services (AWS). It enables us to send notifications or messages to a variety of endpoints or subscribers, such as email addresses, mobile devices, HTTP endpoints, AWS Lambda functions, SQS (Simple Queue Service) queues, and more.

The **s3.yaml** file contains the cloudformation script to create an S3 bucket. 

The **Jenkinsfile** create the stages of the Pipeline. 

**Steps:**
1.	Create an IAM user on AWS free tier account with the following policies 

 <img width="468" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/3582a2d8-2bfd-448b-b09e-ea0cb9c0ff4a">

2.	Connect to an EC2 instance on AWS free tier.
3.	Run the following commands on the server to install java, jenkins and awscli.
   
   **To install java-jdk**
   
   ```
   sudo apt install openjdk-8-jdk -y
   ```

   **Debian package repository of Jenkins to automate installation**
  
  ```
  sudo wget -O /usr/share/keyrings/jenkins-keyring.asc  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

  echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee 
  /etc/apt/sources.list.d/jenkins.list > /dev/null
  ```

**Install jenkins**

   ```
   sudo apt-get update
   sudo apt-get install fontconfig openjdk-17-jre
   sudo apt-get install jenkins
   ```
**Start Jenkins**

```
sudo systemctl start jenkins
sudo systemctl enable Jenkins
sudo systemctl status jenkins
```

7.	After Jenkins start, open the Jenkins console using the public ipv4 address of the instance and using the port 8080.
  ```
  	http://<public-ipv4-address>:8080
  ```

9.	It will prompt for initial password. Navigate to /var/lib/jenkins/secrets/initialAdminPassword to find the initial password.
10.	Create an account on Jenkins.
11.	Install 'aws credentials' plugin by navigating to the available plugins option.
    
    <img width="1345" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/9e62d76d-c4d4-4b78-b1ce-1d9dfd7e2b7e">

12. Setting up jenkins credentials

     <img width="656" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/27a960a5-5ebd-45eb-bd66-ef4101501e17">


13. Click on 'global'
    
    <img width="532" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/a39d0d45-93ce-45bd-bfa5-67270ec2142f">

14.Click on Add Credentials

15. Enter id name ,AWS access key and AWS secret key.
<img width="1352" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/3898e8be-a245-4230-9243-c8bd309ed2f2">






 **Setting up the Jenkins Pipeline**

 1. Click on New item to create a Pipeline. 
 
 <img width="400" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/ddc1a608-1d3f-4b7e-bcae-eebacc096ba1">


2. Enter Pipeline name and select Pipeline. 

   <img width="550" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/caabbbc1-fad9-4678-9b91-5d187d419527">




3. Enter the following details to retrieve the code from Git.
   <img width="1326" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/a2c2b23f-70a3-44e9-a1c1-fd8d875c144b">

4. Specify Jenkinsfile in the script path. Click on Apply and Save. 

   <img width="900" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/44a87837-b933-4234-b38a-fcc7852adfb7">

6. Click on Build Now.

7. The Pipeline will run successfully. A cloudformation stack will be successfully created and a bucket will be created.

<img width="942" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/d7cd8f75-5ffb-4030-8f37-124b4d1e81a8">

Verifying the creation of stack on AWS.

1. A cloudformation stack is created on AWS which will now create a bucket on AWS S3

   <img width="720" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/6431eb5c-c0ad-4c92-9241-0c917c7eaabb">


3. A bucket is created successfully.
   
   <img width="615" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/de8b7eef-0778-44bb-b18e-f1402f34cbd3">

5. SNS Topic is created
   
   <img width="545" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/55b641bb-1171-464f-a459-2cdf520797f2">






