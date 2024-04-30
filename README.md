# Cloudformation-Pipeline-demo

**Problem Statement:**
A Jenkins pipeline has been implemented to streamline the process of automatically creating CloudFormation stacks, which in turn deploy S3 buckets.

The **s3.yaml** file conatins the cloudformation script to create an S3 bucket. 
The **Jenkinsfile** create the stages of the Pipeline. 

**Steps:**
1.	Create an IAM user on AWS free tier account with the following policies 

 <img width="468" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/3582a2d8-2bfd-448b-b09e-ea0cb9c0ff4a">

2.	Connect to an EC2 instance on AWS free tier.
3.	Run the following commands on the server to install java, jenkins and awscli.
   
   To install java-jdk
   sudo apt install openjdk-8-jdk -y
   sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
   4.	echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
   5.	https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
   /etc/apt/sources.list.d/jenkins.list > /dev/null
   6.sudo apt-get update
   7. sudo apt-get install fontconfig openjdk-17-jre
   8. sudo apt-get install jenkins
4.	Sudo systemctl start jenkins
5.	 Sudo systemctl enable Jenkins
6.	Sudo systemctl status jenkins

7.	After Jenkins start, open the Jenkins console using the public ipv4 address of the instance and using the port 8080. 
http://<public-ipv4-address>:8080
8.	It will prompt for initial password. Navigate to /var/lib/jenkins/secrets/initialAdminPassword to find the initial password.
9.	Create an account on Jenkins.
10.	Install 'aws credentials' plugin by navigating to the available plugins option.
    
    <img width="1345" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/9e62d76d-c4d4-4b78-b1ce-1d9dfd7e2b7e">

11. Setting up jenkins credentials

     <img width="656" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/27a960a5-5ebd-45eb-bd66-ef4101501e17">


12.
13. <img width="532" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/a39d0d45-93ce-45bd-bfa5-67270ec2142f">

14.Click on Add Credentials
15. Enter id name ,AWS access key and AWS secret key. 
<img width="1352" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/3898e8be-a245-4230-9243-c8bd309ed2f2">
16. Setting up the Jenkins Pipeline
<img width="293" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/ddc1a608-1d3f-4b7e-bcae-eebacc096ba1">

<img width="550" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/caabbbc1-fad9-4678-9b91-5d187d419527">

<img width="336" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/2f8140c6-87e7-4221-804d-63dfd10c2061">

Click on Build Now.

The Pipeline will run successfully. A cloudformation stack will be successfully created and a bucket will be created. 

