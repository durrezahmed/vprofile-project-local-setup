# RABBITMQ Setup

Login to the `rmq01` VM:

```bash
vagrant ssh rmq01
```

Verify Hosts entry, if entries missing update the it with IP and hostnames:

```bash
cat /etc/hosts
```

Switch to the root user:

```bash
sudo -i
```

Update OS with latest patches:

```bash
yum update -y
```

Set EPEL Repository:

```bash
yum install epel-release -y
```

Install Dependencies:

```bash
sudo yum install wget -y
```

```bash
cd /tmp/
```

```bash
wget http://packages.erlang-solutions.com/erlang-solutions-2.0-1.noarch.rpm
```

```bash
sudo rpm -Uvh erlang-solutions-2.0-1.noarch.rpm
```

```bash
sudo yum -y install erlang socat
```

Install Rabbitmq Server:

```bash
curl -s https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.rpm.sh | sudo bash
```

```bash
sudo yum install rabbitmq-server -y
```

Start & Enable RabbitMQ:

```bash
systemctl start rabbitmq-server
```

```bash
systemctl enable rabbitmq-server
```

```bash
systemctl status rabbitmq-server
```

Config Change:

```bash
sudo sh -c 'echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config'
```

```bash
sudo rabbitmqctl add_user test test
```

```bash
sudo rabbitmqctl set_user_tags test administrator
```

Restart RabbitMQ service:

```bash
systemctl restart rabbitmq-server
```

```bash
systemctl status rabbitmq-server
```

Enabling the firewall and allowing port 25672 to access the rabbitmq permanently:

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
firewall-cmd --zone=public --add-port=25672/tcp --permanent
```

```bash
firewall-cmd --reload
```
