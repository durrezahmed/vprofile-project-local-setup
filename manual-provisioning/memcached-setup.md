# MEMCACHED Setup

Login to the `mc01` VM:

```bash
vagrant ssh mc01
```

Switch to the root user:

```bash
sudo -i
```

Install, start & enable memcache on port 11211:

```bash
yum update -y
```

```bash
yum install epel-release -y
```

```bash
yum install memcached -y
```

Starting & enabling memcached service:

```bash
systemctl start memcached
```

```bash
systemctl enable memcached
```

```bash
systemctl status memcached
```

set the port for memcached to 11211:

```bash
memcached -p 11211 -U 11111 -u memcached -d
```

verify memcached running port:

```bash
ss -tunlp | grep 11211
```

Starting the firewall and allowing the port 11211 to access memcache:

```bash
systemctl enable firewalld
```

```bash
systemctl start firewalld
```

```bash
systemctl status firewalld
```

```bash
firewall-cmd --add-port=11211/tcp --permanent
```

```bash
firewall-cmd --reload
```

```bash
memcached -p 11211 -U 11111 -u memcache -d
```
