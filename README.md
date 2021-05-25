# GitOps-pipeline-code
According to me moving an open source code from git into the production environment by means of automation is called GitOps. 

When we say GitOps pipeline we mean linking all the steps from building the code to deploying it into production. 
Here are some easy steps to follow to create a GitOps pipeline.

PS: I am creating this setup on AWS. 

1. Install JENKINS on your machine. 
sudo wget -O /etc/yum.repos.d/jenkins.repo     https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum install jenkins -y 

2. Open Jenkins Dashboard
http://<IP>:8080

Note: If you are doing this setup on AWS, make sure to configure Security groups that allows port 8080

3. Install additional plugins - Docker, Git, Docker pipeline
  
4. Give jenkins user permission for using docker socket of the underlying machine. This step is performed as Jenkins needs a machine to launch its docker container. 
 sudo visudo -f /etc/sudoers
  Add following line at the end of the visudo file.
 jenkins ALL= NOPASSWD: ALL
   This will also allow the Jenkins User to run su (super user) commands without the need to input a password. Once this is done, switch to the Jenkins user on the terminal.
 sudo su - jenkins
  
5. Create new Item as pipeline

6. Enter  the project URL
  Under Pipeline section select Pipeline script from SCM and enter repository url(By configuring this setting we are telling jenkins to look into this repository for Jenkinsfile required to build pipeline.)
7. Don't change Script path. 
8. Click Save. 
  
