# NGINX Setup

Note: If some problem arises during the setup process, restart the vm and ssh into it.

Login to the `web01` VM:

```bash
vagrant ssh web01
```

Verify Hosts entry, if entries missing update the it with IP and hostnames:

```bash
cat /etc/hosts
```

Update OS with latest patches:

```bash
sudo apt update && sudo apt upgrade -y
```

Login as the root user:

```bash
sudo -i
```

Install nginx:

```bash
apt install nginx -y
```

Create Nginx conf file with below content:

```bash
vi /etc/nginx/sites-available/vproapp
```

Enter the following inside the file:

```bash
# for our setup
upstream vproapp {
server app01:8080;
}
server {
listen 80;
location / {
proxy_pass http://vproapp;
}
}

# if multiple servers
upstream vproapp {
server app01:8080;
server app02:8080;
server app02:8080;
}
server {
listen 80;
location / {
proxy_pass http://vproapp;
}
}
```

Remove default nginx conf:

```bash
rm -rf /etc/nginx/sites-enabled/default
```

Create link to activate website:

```bash
ln -s /etc/nginx/sites-available/vproapp /etc/nginx/sites-enabled/vproapp
```

Restart Nginx:

```bash
systemctl restart nginx
```

```bash
systemctl status nginx
```
