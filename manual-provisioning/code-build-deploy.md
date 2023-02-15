# CODE BUILD & DEPLOY (app01)

Login to the `app01` VM:

```bash
vagrant ssh app01
```

Download Source code:

```bash
git clone https://github.com/durrezahmed/vprofile-project-devops.git
```

```bash
ls
```

Update configuration:

```bash
cd vprofile-project-devops
```

```bash
git status
```

```bash
vim src/main/resources/application.properties
```

Update file with backend server details:

```bash
#JDBC Configutation for Database Connection
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://db01:3306/accounts?useUnicode=true&characterEncoding=UTF-8&zeroDateTimeBehavior=convertToNull
jdbc.username=admin
jdbc.password=admin123

#Memcached Configuration For Active and StandBy Host
#For Active Host
memcached.active.host=mc01
memcached.active.port=11211

#For StandBy Host
memcached.standBy.host=127.0.0.2
memcached.standBy.port=11211

#RabbitMq Configuration
rabbitmq.address=rmq01
rabbitmq.port=5672
rabbitmq.username=test
rabbitmq.password=test

#Elasticesearch Configuration
elasticsearch.host =192.168.1.85
elasticsearch.port =9300
elasticsearch.cluster=vprofile
elasticsearch.node=vprofilenode
```

### Build code

Run below command inside the repository (vprofile-project-devops):

```bash
mvn install
```

```bash
ls
```

```bash
cd target/
```

```bash
ls
```

Deploy artifact:

```bash
systemctl stop tomcat
```

```bash
systemctl status tomcat
```

```bash
rm -rf /usr/local/tomcat8/webapps/ROOT*
```

```bash
cd ..
```

```bash
cp target/vprofile-v2.war /usr/local/tomcat8/webapps/ROOT.war
```

```bash
ls /usr/local/tomcat8/webapps/
```

```bash
systemctl start tomcat
```

```bash
exit
```

```bash
chown tomcat.tomcat usr/local/tomcat8/webapps -R
```

```bash
systemctl restart tomcat
```
