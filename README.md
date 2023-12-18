# Tomcat
Tomcat is an open-source web server and servlet. The Apache Software Foundation has developed it. It is used widely for hosting Java-based applications on the web. It is built on Java technologies and implements the Java Servlet and JavaServer Pages (JSP) specifications.

# Tomcat-Setup Guide
## Prerequisites
1. EC2 Instance 
   - With Internet Access
   - Security Group with Port `8080` open for internet.
  
## Install Tomcat
   Get the latest version of tomcat from ``` https://tomcat.apache.org/ ```

### Run the below commands to install Java and Tomcat
 
 1. Install Java
   ```
   sudo yum  install java-11-openjdk -y 
   ```
 2. Verify Java is Installed
   ```
    java -version
   ```
 3. Download binary Tomcat file from offical documentaion
   ```
      sudo wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.83/bin/apache-tomcat-9.0.83.tar.gz
   ```
 4. Copy and extract gz file to /opt/tomcat Directory
   ```
     sudo tar -xvzf apache-tomcat-9.0.83-bin.tar.gz -C /opt/tomcat/
   ```
 5. Create user for Tomcat Application and Setup Password.
 6. Change owner permission of /opt/tomcat directory to tomcat user and Login to tomcat user.
   ```
     sudo chown -R <UserName>:<UserName> /opt/tomcat/
   ```
 7. Create symbolic link to startup.sh and shutdown.sh file so that tomcat server start and stop can be executed from any directory. 
   ```
     sudo ln -s /opt/tomcat/apache-tomcat-9.0.83/bin/startup.sh /usr/bin/tomcatup
     sudo ln -s /opt/tomcat/apache-tomcat-9.0.83/bin/shutdown.sh /usr/bin/tomcatdown
  ```
# Tomcat War file deployment Configs
   To have access to the dashboard the admin user needs the manager-gui role. In order for Tomcat to accept remote deployments, we have to add a user with the role managerscript.
   To do so, edit the file ../conf/tomcat-users.xml and add the following lines:
   In this case : add below configuration in file /opt/tomcat/apache-tomcat-9.0.83/conf/tomcat-users.xml
  ```
   <?xml version="1.0" encoding="UTF-8"?>
   <tomcat-users>
       <role rolename="manager-gui"/>
       <role rolename="manager-script"/>
       <user username="tomcatmgr" password="manager" roles="manager-gui, manager-script"/>
    </tomcat-users>
   ```
  To have access from local host.
    Edit the RemoteAddrValve under this file /opt/tomcat/apache-tomcat-9.0.35/webapps/manager/METAINF/context.xml to allow all.
    Replace this value ``allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> `` with ```allow=".*" /> ```
# Now Start the tomcat.
   ```
   tomcatup
   ```
  By default tomcat runs at port `8080`, You can access tomcat at 
   ``` http://YOUR-SERVER-PUBLIC-IP:8080 ```

   

