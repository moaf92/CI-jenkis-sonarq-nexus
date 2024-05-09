# ci-jenkis-sonar-nexus

# Prerequisites

- initialize three ec2 instances with SG to set up the below servers 
- Setup SonarQube server by using user data
- Setup Nexus server by using user data
- Setup Jenkins server by using user data
- Install nexus, sonarqube, git and maven plugins
- integrate Jenkins with sonarqube and nexus
- Write Pipeline script
- Set notification

# Tools
 
- Jenkins
- Maven
- SonarQube
- Nexus Sonatype
- aws 
- Slack Notification


# Aim Of This Project

After a developer commit his code to GitHub repo as soon as the code change Jenkins will detect the change and fetch the code using git tool whenever there is a change after that in the pipeline the code will be build so we will use maven to build the code because its java code next we will conduct unit test again by using maven after this we will use another kind of code analysis called sonarqube scanner to scan the code it searchers if there is any bugs through feature called quality gates and after this it uploads the results to sonarqube server if the scan passed now we have verified copy of artifact which we can distributed to be deployed on servers but before we have artifact that will be versioned and  uploaded to nexus repo



# Steps To Execute

- create Jenkins server on aws using ec2 instance with security group allowing inbound trrafic on port 8080 and 22 for ssh and install Jenkins using user 
  data , after this we have to 'cat' to '/var/lib/jenkins/secrets/initialAdminPassword' this file contain initial password to unlock jenkins

- we will need configure tools after installing them as plugins and mention it as global configuration . we will need 'oracle jdk 11' and mention its path 
  '/usr/lib/jvm/java-1.11.0-openjdk-amd64' and 'maven'

- create nexus server on aws using ec2 instance with security group allowing inbound trrafic on port 8081 and 22 for ssh and install nexus using user data .


- To enable nexus repo we have to login to the server and to do that we have too ssh to machine to this file '/opt/nexus/sonatype- 
  work/nexus3/admin.password' to show the initial password of logging into nexus server 


- create SonarQube server on aws using ec2 instance with security group allowing inbound trrafic on port 80 'nginx service' which will route traffic to port 
  9000 of sonarqube and 22 for ssh and install SonarQube server using user data .


- Back to Jenkins time for installing: nexus artifact uploader, SonarQube scanner, build timestamp, pipeline maven and pipeline utility steps Plugins

- Now time to build our pipeline

- after install SonarQube plugin now we have to install and configure SonarQube scanner tool to integrate Jenkins with SonarQube server by mention the sonar 
  public url of the host ec2 and by authentication token that will be created from SonarQube server and set it as credentials in jenkins

- after pushing reports to SQ server we will go to quality gates and create one for our project. but first we have to create webhook to make SonarQube send 
  information about analytical reports to Jenkins by mention the private url of Jenkins instance '/sonarqube-webhook'

- Now time to upload our artifact to nexus repository  but we have to create a hosted maven repo on nexus to store the artifact and from Jenkins we will set 
  up credentials so that plugin can use that credential
 
- finally for notification we have to install slack notification plugin , create workspace and channel , we have to create token in order to Jenkins can 
  authenticate to workspace
