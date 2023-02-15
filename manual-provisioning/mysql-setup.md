# MYSQL Setup

Login to the `db01` VM:

```bash
vagrant ssh db01
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

Set Repository:

```bash
yum install epel-release -y
```

Install Maria DB Package:
(we will be using mariadb for rpm based os and mysql for debian based os, basically both are same)

```bash
yum install git mariadb-server -y
```

Starting & enabling mariadb-server:

```bash
systemctl start mariadb
```

```bash
systemctl enable mariadb
```

RUN mysql secure installation script:

```bash
mysql_secure_installation
```

```bash
# NOTE: Set db root password, I will be using admin123 as password

# Set root password? [Y/n] Y
# New password:
# Re-enter new password:
# Password updated successfully!
# Reloading privilege tables..
# ... Success!
# By default, a MariaDB installation has an anonymous user, allowing anyone
# to log into MariaDB without having to have a user account created for
# them. This is intended only for testing, and to make the installation
# go a bit smoother. You should remove them before moving into a
# production environment.
# Remove anonymous users? [Y/n] Y
# ... Success!
# Normally, root should only be allowed to connect from 'localhost'. This
# ensures that someone cannot guess at the root password from the network
# Disallow root login remotely? [Y/n] n
# ... skipping.
# By default, MariaDB comes with a database named 'test' that anyone can
# access. This is also intended only for testing, and should be removed
# before moving into a production environment.
# Remove test database and access to it? [Y/n] Y
# - Dropping test database...
# ... Success!
# - Removing privileges on test database...
# ... Success!
# Reloading the privilege tables will ensure that all changes made so far
# will take effect immediately.
# Reload privilege tables now? [Y/n] Y
# ... Success!
```

Set DB name and users:

```bash
mysql -u root -padmin123
```

Enter every command individually in mysql sheel:

```bash
mysql> create database accounts;
mysql> grant all privileges on accounts.* TO 'admin'@'%' identified by 'admin123';
mysql> FLUSH PRIVILEGES;
mysql> exit;
```

Download Source code & Initialize Database:

```bash
git clone https://github.com/durrezahmed/vprofile-project-devops.git
```

```bash
cd vprofile-project-devops
```

```bash
mysql -u root -padmin123 accounts < src/main/resources/db_backup.sql
```

```bash
mysql -u root -padmin123 accounts
```

```bash
mysql> show tables;
```

Restart mariadb-server:

```bash
systemctl restart mariadb
```

Starting the firewall and allowing the mariadb to access from port no. 3306:

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
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```

```bash
firewall-cmd --reload
```

```bash
systemctl restart mariadb
```
