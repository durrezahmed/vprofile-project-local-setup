# TOMCAT Setup

Login to the `app01` VM:

```bash
vagrant ssh app01
```

Verify Hosts entry, if entries missing update the it with IP and hostnames:

```bash
cat /etc/hosts
```

Update OS with latest patches:

```bash
yum update -y
```

Set Repository:

```bash
yum install epel-release -y
```

Install Dependencies:

```bash
yum install java-1.8.0-openjdk -y
```

```bash
yum install git maven wget -y
```

Change dir to /tmp:

```bash
cd /tmp/
```

Download & Tomcat Package:

```bash
wget https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.37/bin/apache-tomcat-8.5.37.tar.gz
```

```bash
tar xzvf apache-tomcat-8.5.37.tar.gz
```

Add tomcat user:

```bash
useradd --home-dir /usr/local/tomcat8 --shell /sbin/nologin tomcat
```

```bash
id tomcat
```

```bash
ls /usr/local/tomcat8/
```

Copy data to tomcat home dir:

```bash
cp -r /tmp/apache-tomcat-8.5.37/* /usr/local/tomcat8/
```

Make tomcat user owner of tomcat home dir:

```bash
chown -R tomcat.tomcat /usr/local/tomcat8
```

```bash
ls -ld /usr/local/tomcat8/
```

```bash
ls -l /usr/local/tomcat8/
```

Setup systemd for tomcat: (Update file with following content)

```bash
vi /etc/systemd/system/tomcat.service
```

```bash
cat /etc/systemd/system/tomcat.service
```

copy and paste this content in tomcat.service file opened in vi editor:

```bash
[Unit]
Description=Tomcat
After=network.target

[Service]
User=tomcat
WorkingDirectory=/usr/local/tomcat8
Environment=JRE_HOME=/usr/lib/jvm/jre
Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=CATALINA_HOME=/usr/local/tomcat8
Environment=CATALINE_BASE=/usr/local/tomcat8
ExecStart=/usr/local/tomcat8/bin/catalina.sh run
ExecStop=/usr/local/tomcat8/bin/shutdown.sh
SyslogIdentifier=tomcat-%i

[Install]
WantedBy=multi-user.target
```

```bash
systemctl daemon-reload
```

```bash
systemctl start tomcat
```

```bash
systemctl enable tomcat
```

```bash
systemctl status tomcat
```

Enabling the firewall and allowing port 8080 to access the tomcat:

```bash
systemctl start firewalld
```

```bash
systemctl enable firewalld
```

```bash
firewall-cmd --get-active-zones
```

```bash
firewall-cmd --zone=public --add-port=8080/tcp --permanent
```

```bash
firewall-cmd --reload
```
