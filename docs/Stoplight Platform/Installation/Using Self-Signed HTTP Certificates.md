# Using Self-Signed HTTPS Certificates

This article covers how to work with Stoplight and self-signed (or internally-signed) HTTPS certificates.

Whether you are using a self-signed certificate for your Stoplight installation or you are trying to connect to an external service that uses a self-signed certificate, you'll need to add the certificate to the Stoplight processes "trust store" in order for it to be marked as safe. To do this, you will need to expose the certificate to the Stoplight process under an environment variable.

> Please note that the instructions covered in this article refer to both self-signed certificates (ie, certificates not signed by a CA) as well as "internally-signed certificates" (ie, certificates signed by an internal CA). If you are working with a true self-signed certificate, then use that certificate in place of an internal CA root certificate.

## Container-based Installations
For Docker-based or container-based installations, you will need to mount the self-signed (or custom CA root) certificate inside the container in order to expose it to the running process. This involves:

- Creating a volume mount that allows for the Stoplight process.
- Setting the [NODE_EXTRA_CA_CERTS](https://nodejs.org/api/cli.html#cli_node_extra_ca_certs_file) environment variable to the local path of the CA certificate.

For example, using the "docker run" command from the [Docker Installation Guide](https://support.stoplight.io/hc/en-us/articles/360032728292):

```bash
docker run [...] -v /my/custom/certificate.pem:/etc/ssl/custom.pem -e NODE_EXTRA_CA_CERTS=/etc/ssl/custom.pem [...]
```

Where `/my/custom/certificate.pem` path above is the path on the *host machine* where your certificate resides. You will need to update the path to match your local setup.

## RPM-based Installations
For RPM-based installations of Stoplight, you will need expose the self-signed (or custom CA root) certificate to the frontend and backend processes. This requires setting the [NODE_EXTRA_CA_CERTS](https://nodejs.org/api/cli.html#cli_node_extra_ca_certs_file) environment variable to the local path of the certificate.

For example, if your certificate resides at the location `/my/custom/certificate.pem`, then you will need to set the following value in both service configurations:

```bash
NODE_EXTRA_CA_CERTS=/my/custom/certificate.pem
```

The variable above will need to be updated to match your local setup, and be exposed through both configurations:

- ```bash
/etc/stoplight-frontend/stoplight-frontend.cfg


- ```bash
/etc/stoplight-backend/stoplight-backend.cfg

<!--theme: warning-->
> **Don't forget to restart the services if they are already running**.