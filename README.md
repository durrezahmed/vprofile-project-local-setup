# DevOps Project - Vprofile Project Local Setup

This is DevOps project for vprofile app local setup using Manual and Automated Provisioning.

## Manual Provisioning

### Usage

#### Clone Repository:

```bash
git clone https://github.com/durrezahmed/vprofile-project-local-setup.git
```

```bash
cd vprofile-project-local-setup/manual-provisioning
```

#### Run the following Command to Start the VMs:

```bash
vagrant up
```

#### Run the following Command to check the Status of the VMs:

```bash
vagrant status
```

#### Then Run all the Commands from the Files in the following order:

- mysql-setup.md
- memcached-setup.md
- rabbitmq-setup.md
- tomcat-setup.md
- code-build-deploy.md

The interface of the vprofile app is then available at the IP Address of the Nginx VM `192.168.56.11` or by using the hostname `web01` in the browser.

## Automated Provisioning

### Usage

#### Clone Repository:

```bash
git clone https://github.com/durrezahmed/vprofile-project-local-setup.git
```

```bash
cd vprofile-project-local-setup/automated-provisioning
```

#### Run the following Command to Start the Automated Provisioning of the VMs:

```bash
vagrant up
```

#### Run the following Command to check the Status of the VMs:

```bash
vagrant status
```

The interface of the vprofile app is then available at the IP Address of the Nginx VM `192.168.56.11` or by using the hostname `web01` in the browser.
