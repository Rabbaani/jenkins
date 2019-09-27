# jenkins with sonarqube

SonarQube Installation

The pre-requisite for instalaation of java

- JAVA
- MAVEN
 
JAVA INSTALLATION 

# cd /opt

# yum install java-1.8.0-openjdk-devel -y

# echo $JAVA_HOME

# file $(which java)

output wil be like this /etc/alternatives/java


# file /etc/alternatives/java
output wil be like this /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-1.el8_0.x86_64/jre/bin/java

# file /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-1.el8_0.x86_64/jre/bin/java

# export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-1.el8_0.x86_64/jre/bin/java

# export PATH=$JAVA_HOME/bin:$PATH

# echo $JAVA_HOME

# echo $PATH


MAVEN INSTALLATION


# cd /opt

# yum install wget -y

# wget http://apachemirror.wuchna.com/maven/maven-3/3.6.2/binaries/apache-maven-3.6.2-bin.tar.gz

# tar -xvf apache-maven-3.6.2-bin.tar.gz

# export M2_HOME=/opt/apache-maven-3.6.2 >> ~/.bash_profile

# export M2_HOME=/opt/apache-maven-3.6.2 >> /etc/profile

# export PATH=$PATH:$M2_HOME/bin >> ~/.bash_profile

# source ~/.bash_profile

# mvn -version

if you got error will get like this 

The JAVA_HOME environment variable is not defined correctly
This environment variable is needed to run this program
NB: JAVA_HOME should point to a JDK not a JRE

# echo $JAVA_HOME

 The output will be /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-1.el8_0.x86_64/jre/bin/java

# export JAVA_HOME= paste the above but remove /bin/java

# mvn -version


SONARQUBE
go to this website https://www.sonarqube.org/downloads/
 
# yum install wget unzip -y
# wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.6.zip
# unzip sonarqube-7.6.zip
# useradd <username>
# visudo
here goto 
root ALL=(ALL)   ALL
<username> ALL=(ALL)   NOPASSWD:ALL

If we dont gine NOPASSWD here whenever yu hit the root it will ask password
NOPASSWD:ALL- it wont ask password

Here we cannot run sonarqube in root due to some security issue. so we have to create a user.
we will give root ownership permissions and all read write and xecute permissions.

# chown -R <username>:<username> /opt/sonarqube-7.6
# chmod -R 777 /opt/sonarqube-7.6
# su - <username> ---switching the new user
# cd /opt/sonarqube-7.6.1
# cd bin
# ls
# cd linux-x84-64
# ls
# ./sonar.sh start ---to start the sonar we have to be in that directory
# ./sonar.sh status

now goto the instance change the port number in security groups
now hit the ip:9000 in search bar 

login details as
     username=admin
     password=admin

after logging change the password
Administration-->security-->yes-->save

SONARQUBE with MAVEN Integration

# install JAVA
# install Maven
# install SonarQube
# install git -y
# git clone <git clone path>
# cd maven-web-applications
# mvn clean package

here a Target folder will be created in that foldera .war file will generated

Goto the pom.xml
# cd /opt/maven-web-applications
# vi pom.xml

scroll down to properties there yu can find sonar propertiesand edit 
provide the <sonar.host.url>url link</sonar.host.url>
            <sonar.login>username</sonar.login>
            <sonar.password>password</sonar.password>
# mvn sonar:sonar

Here a maven-web-applications file will be generated in SonarQube site
