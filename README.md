# Cloudformation-Pipeline-demo

Automation using Jenkins
Problem Statement:

A Jenkins pipeline has been implemented to streamline the process of automatically creating CloudFormation stacks, which in turn deploy S3 buckets.

Steps:
1.	Create an IAM user on AWS free tier account with the following policies 

 <img width="468" alt="image" src="https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/3582a2d8-2bfd-448b-b09e-ea0cb9c0ff4a">


2.	Connect to an EC2 instance on AWS free tier. 
3.	Run the following commands on the server to install java, jenkins and awscli. 
1.	sudo apt update
2.	sudo apt install openjdk-8-jdk -y
3.	sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
4.	echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
5.	    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
   /etc/apt/sources.list.d/jenkins.list > /dev/null
   sudo apt-get update
  sudo apt-get install fontconfig openjdk-17-jre
  sudo apt-get install jenkins
6.	Sudo systemctl start jenkins
7.	 Sudo systemctl enable Jenkins
8.	Sudo systemctl status jenkins

4.	After Jenkins start, open the Jenkins console using the public ipv4 address of the instance and using the port 8080. 
http://<public-ipv4-address>:8080
5.	It will prompt for initial password. Navigate to /var/lib/jenkins/secrets/initialAdminPassword to find the initial password.
6.	Create an account on Jenkins.


![image](https://github.com/anisha16/Cloudformation-Pipeline-demo/assets/53351266/33a36b95-9922-4491-8972-91c0d7a31865)
