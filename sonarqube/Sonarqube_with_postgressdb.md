# Sonarqube Setup

SonarQube is an open-source static testing analysis software, it is used by developers to manage source code quality and consistency.

## 🧰 Prerequisites
1. Need an EC2 instance (t2.medium)
2. Install Java-11

## Update the server
    sudo yum update -y
    
## Install java 11
    sudo amazon-linux-extras install java-openjdk11
## Setup PostgreSQL 10 Database For SonarQube
    amazon-linux-extras install postgresql10 vim epel -y
    yum install -y postgresql-server postgresql-devel
    /usr/bin/postgresql-setup --initdb
  
## Need to change config file

vi /var/lib/pgsql/data/pg_hba.conf

Replace Method name "peer" to "md5"

Enable  postgresql:
    
    systemctl enable postgresql
    
Start postgresql:

    systemctl start postgresql
  
  Login into Database
	  
    su - postgres
You can get into Postgres console by typing
	  
    psql
    
Create a sonarqubedb database
	  
    create database sonarqubedb;
    
Create the sonarqube DB user with a strongly encrypted password
	  
    create user sonar with encrypted password 'sonar';
    
Next, grant all privileges to sonrqube user on sonarqubedb
	  
    grant all privileges on database sonarqubedb to sonar;
    
Exit the psql prompt using the following command
	  
    \q
    
Switch to your sudo user using the exit command
	  
    exit
Added below entries in `/etc/sysctl.conf`
  ```sh 
  vm.max_map_count=524288
  fs.file-max=131072
  ulimit -n 131072
  ulimit -u 8192
  ```
 Add below entries in `/etc/security/limits.conf`
  ```sh 
  sonarqube   -   nofile   131072
  sonarqube   -   nproc    8192
  ```
  1. reboot the server 
  ```sh 
  init 6
  ```
  ============================================================
  
 Download [soarnqube](https://www.sonarqube.org/downloads/) and extract it.   
  ```sh 
  cd /opt/
  wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.2.46101.zip
  unzip sonarqube-8.9.2.46101.zip
  mv   sonarqube-8.9.2.46101 sonarqube
  ```
 ## Open /opt/sonarqube/conf/sonar.properties file

 sudo vi /opt/sonarqube/conf/sonar.properties 
```sh
sonar.jdbc.username=sonar
sonar.jdbc.password=sonar
sonar.jdbc.url=jdbc:postgresql://localhost/sonarqubedb
sonar.web.host=0.0.0.0
sonar.web.port=9000
sonar.search.javaOpts=-Xmx512m -Xms512m -XX:MaxDirectMemorySize=256m -XX:+HeapDumpOnOutOfMemoryError
```
## Create sonarqube.service file:

 Create a `/etc/systemd/system/sonarqube.service` file start sonarqube service at the boot time 
  ```sh   
  cat >> /etc/systemd/system/sonarqube.service <<EOL
  [Unit]
  Description=SonarQube service
  After=syslog.target network.target

  [Service]
  Type=forking
  User=sonar
  Group=sonar
  PermissionsStartOnly=true
  ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start 
  ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop
  StandardOutput=syslog
  LimitNOFILE=65536
  LimitNPROC=4096
  TimeoutStartSec=5
  Restart=always

  [Install]
  WantedBy=multi-user.target
  EOL
  ```
  
  Add sonar user and grant ownership to /opt/sonarqube directory 
  
  ```sh 
  useradd -d /opt/sonarqube sonar
  chown -R sonar:sonar /opt/sonarqube
  ```
  
 Reload the demon and start sonarqube service 
  ```sh 
  systemctl daemon-reload 
  systemctl start sonarqube.service 
  ```


  


