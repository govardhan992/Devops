# Install Jenkins on aws Linux

Jenkins is a self-contained Java-based program, ready to run out-of-the-box, with packages for Windows, Mac OS X and other Unix-like operating systems. As an extensible automation server, Jenkins can be used as a simple CI server or turned into the continuous delivery hub for any projects.

## Prerequisites:
	1. Ec2 instance (t2.micro)
  2. Java 11 should be installed
  
## Install Jenkins:

   1. Get the latest version of jenkins from  https://pkg.jenkins.io/redhat-stable/ and install
   
    Run following commands:    
    ```sh
    sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
    sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
    sudo amazon-linux-extras install java-openjdk11 -y
    yum install jenkins -y
     ```
     
    Start Jenkins:      
     ```sh
     service jenkins start
     ```








