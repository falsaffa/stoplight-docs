# Installing With RPMs

> This article is for Stoplight current and prospective customers. If you are not yet a customer and would like to run Stoplight on premises, please don't hesitate to get in touch with our Sales team by sending an email to [sales@stoplight.io](sales@stoplight.io).

This guide covers how to install the Stoplight Platform on any RHEL/CentOS Linux system using the RPM package format.

The Stoplight Platform is composed of two separate packages when installed via RPM:

- The *front-end*, which serves the Stoplight web application UI.
- The *back-end*, which is the backing API for the front-end application. It's the back-end that ultimately connects to and writes data to the database.

## Prerequisites
Prior to installing the RPM package, you will need to:

- Have access to a RHEL/CentOS 6, 7, or 8 system
- Have access to (or know how to install and configure) a running PostgreSQL v10 server
- Install NodeJS v12.16.x LTS
- Have a set of credentials for accessing the Stoplight RPM Repository

## Networking Requirements
The default ports for the front-end and back-end services are as follows:

- The front-end default TCP port is **4050**
  - This service must receive traffic from: 
    - Clients (ie, web browsers or Studio desktop clients)
  - This service must initiate traffic to:
    - The back-end service
- The back-end default TCP port is **4060**
  - This service must receive traffic from:
    - The front-end service
    - Clients (ie, web browsers or Studio desktop clients)
- This service must initiate traffic to:
  - PostgreSQL

Both ports can be customized using the **PORT** configuration/environment variable.

> If you require SSL encryption, you will need to also provision a proxy server ([nginx](https://nginx.org/en/), for example) for terminating SSL/TLS connections.

## Installing NodeJS
Both Stoplight components require NodeJS LTS version v12.16. If you do not have access to a NodeJS package in your default repositories, you can install it with the command:

```bash
sudo rpm -Uvh https://rpm.nodesource.com/pub_12.x/el/7/x86_64/nodejs-12.16.1-1nodesource.x86_64.rpm
```

Once the installation has completed, verify the version installed with the command:

```bash
$ node --version
v12.16.1
```

## Configuring the Stoplight Package Repo
You can setup the Stoplight package repo by copying-and-pasting the contents below into a terminal:

```bash
# expose credentials to environment first
REPO_USERNAME="myusername"
REPO_PASSWORD="mypassword"

# write credentials to repo file
cat <<EOF | sudo tee /etc/yum.repos.d/stoplight.repo
[stoplight]
name=Stoplight Package Repository
baseurl=https://$REPO_USERNAME:$REPO_PASSWORD@pkg.stoplight.io/rpm
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://pkg.stoplight.io/stoplight.key
EOF
```
<!--theme: warning-->
> Make sure that your repository credentials are set before issuing the "cat" command above.

## Installation
Once the prerequisites are met, you can install the packages with the command:

```bash
sudo yum install stoplight-frontend stoplight-backend -y
```

Once installed, you can start the services with the command:

```bash
sudo systemctl enable stoplight-{frontend,backend}
sudo systemctl start stoplight-{frontend,backend}
```

Once started, you can see the status of the service using the command:

```bash
sudo systemctl status stoplight-backend
```

## Configuring
The configuration files for the services are located at:

```bash
/etc/stoplight-frontend/stoplight-frontend.cfg
/etc/stoplight-backend/stoplight-backend.cfg
```

Any changes to the configuration will require a service restart in order to take effect.

```bash
sudo systemctl restart stoplight-{frontend,backend}
```

Please see the configuration guide [here](https://support.stoplight.io/hc/en-us/articles/360036239191) for a full reference of all available configuration options.

## Logging
By default the services log directly to journald. You can see the logs for each respective service with the command:

```bash
journalctl -f -u stoplight-frontend
journalctl -f -u stoplight-backend
```
 