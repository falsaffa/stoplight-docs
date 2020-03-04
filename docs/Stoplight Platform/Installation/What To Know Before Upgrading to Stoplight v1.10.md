# What To Know Before Upgrading to Stoplight v1.10

## With the Stoplight v1.10 release, there have been a few changes to how Stoplight is run.

> **Please note** that this article is specifically geared for administrators of Stoplight who have installed via [RPM](https://support.stoplight.io/hc/en-us/articles/360033742792). Administrators of Stoplight who installed with Stoplight-provided [containers](https://support.stoplight.io/hc/en-us/articles/360032728292) will be updated automatically, with no manual intervention required.

## NodeJS Upgrade to v12.16
The NodeJS requirement has been upgraded from v10.16 to v12.16. [Both are LTS versions](https://nodejs.org/en/about/releases/) of the NodeJS project, however this extends the NodeJS version support through April of 2022.

If you do not have a NodeJS v12.16 version available, you can install one using the command below:

```bash
sudo rpm -Uvh https://rpm.nodesource.com/pub_12.x/el/7/x86_64/nodejs-12.16.1-1nodesource.x86_64.rpm
```

## Addition of the Exporter Service
With v1.10, the **Exporter** service has been added to the Stoplight run-time. This service is responsible for serving, de-referencing, and bundling dependencies for JSON Schema and OpenAPI files.

To install this service, you will also need the **stoplight-exporter** RPM package:

```bash
sudo yum install -y stoplight-exporter
```

This package can be configured via the **/etc/stoplight-exporter/stoplight-exporter.cfg** file, and takes a single configuration option:

```bash
# this must be the same URL provided to the Stoplight API service
SL_POSTGRES_URL=postgres://user:password@postgres.example.com:5432/stoplight
```

Once configured, start the service with:

```bash
sudo systemctl start stoplight-exporter
```