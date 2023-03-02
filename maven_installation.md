# Install & configure Maven build tool on Jenkins

## Prerequisites

 1. Jenkins server
 
## Install Maven on Jenkins: 
 
Download maven packages  https://maven.apache.org/download.cgi onto Jenkins server. In this case I am using /opt/maven as my installation director.

Run Following commands
  
      mkdir /opt/maven
      cd /opt/maven
      wget https://dlcdn.apache.org/maven/maven-3/3.9.0/binaries/apache-maven-3.9.0-bin.tar.gz
      tar -zvxf apache-maven-3.9.0-bin.tar.gz
      
## Setup M2_HOME and M2 paths in .bash_profile of user and add these to path variable
      
  vi ~/.bash_profile
  
       M2_HOME=/etc/maven/apache-maven-3.9.0
       M2=$M2_HOME/bin
       PAHT=<Existing_PATH>:$M2_HOME:$M2
       
## Check point

 logoff and login to check maven version 
     
         mvn -version




