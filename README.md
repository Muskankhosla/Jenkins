# Jenkins

Jenkins is an open source continuous integration/continuous delivery and deployment (CI/CD) automationwritten in the Java programming language. It is used to implement CI/CD workflows, called pipelines.

**Pipelines** automate testing and reporting on isolated changes in a larger code base

To operate Jenkins, pipelines are created.A pipeline is a series of steps the Jenkins server will take to perform the required tasks of the CI/CD process. These are stored in a plain text ** Jenkinsfile**. The Jenkinsfile uses a curly bracket syntax that looks similar to JSON.

**Plugins**
A plugin is an enhancement to the Jenkins system. They help extend Jenkins capabilities and integrated Jenkins with other software. Plugins help to integrate other developer tools into the Jenkins environment, add new user interface elements to the Jenkins Web UI, help with administration of Jenkins, and enhance Jenkins for build and source code management. 

**Installation on EC2 Instance**
YouTube Video -> https://www.youtube.com/watch?v=zZfhAXfBvVA&list=RDCMUCnnQ3ybuyFdzvgv2Ky5jnAA&index=1

Install Jenkins, configure Docker as agent, set up cicd, deploy applications to k8s and much more.

**AWS EC2 Instance**<br>
Go to AWS Console<br>
Instances(running)<br>
Launch instances<br>


**Install Jenkins**<br>
Pre-Requisites:<br>

**Java (JDK)**<br>
Run the below commands to install Java and Jenkins<br>
<br>
Install Java<br>
sudo apt update<br>
sudo apt install openjdk-11-jre<br>
Verify Java is Installed<br>
java -version<br>
Now, you can proceed with installing Jenkins<br>

curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null<br>
sudo apt-get update<br>
sudo apt-get install jenkins<br>

**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.<br>

EC2 > Instances > Click on<br>
In the bottom tabs -> Click on Security<br>
Security groups<br>
Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).<br>


Login to Jenkins using the below URL:<br>
http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]<br>

Note: If you are not interested in allowing All Traffic to your EC2 instance<br>
1. Delete the inbound traffic rule for your instance<br>
2.  2. Edit the inbound traffic rule to only allow custom TCP port 8080<br>

After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password<br>
Click on Install suggested plugins<br>
Wait for the Jenkins to Install suggested plugins<br>
Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]<br>

Jenkins Installation is Successful. You can now starting using the Jenkins<br>

Install the Docker Pipeline plugin in Jenkins:<br>
Log in to Jenkins.<br>
Go to Manage Jenkins > Manage Plugins.<br>
In the Available tab, search for "Docker Pipeline".<br>
Select the plugin and click the Install button.<br>
Restart Jenkins after the plugin is installed.<br>

Wait for the Jenkins to be restarted.<br>

Docker Slave Configuration<br>
Run the below command to Install Docker<br>

sudo apt update<br>
sudo apt install docker.io<br>
Grant Jenkins user and Ubuntu user permission to docker deamon.<br>
sudo su - <br>
usermod -aG docker jenkins<br>
usermod -aG docker ubuntu<br>
systemctl restart docker<br>
Once you are done with the above steps, it is better to restart Jenkins.<br>

http://<ec2-instance-public-ip>:8080/restart<br>
The docker agent configuration is now successful.<br>
