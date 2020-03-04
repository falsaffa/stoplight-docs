# Troubleshooting

## Finding Your Version of Stoplight

### Docker Image Version
If you need to find the version of your Docker image, run the shell command:

```bash
docker logs stoplight-platform 2>&1 | grep 'Platform version'
```

For example:

```bash
$ docker logs stoplight-platform 2>&1 | grep 'Platform version'
[INFO] Platform version: 1.3.0
```

Or by checking the Docker image tag that was used to retrieve Stoplight from the Docker registry.

### RPM Version
When running from RPM, each RPM component should be labeled with the version information. You can find the versions of each by running the shell command:

```bash
rpm -qa | grep stoplight
```