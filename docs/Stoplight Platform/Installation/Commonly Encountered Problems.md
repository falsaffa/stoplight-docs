# Commonly Encountered Problems

## When adding an external service, I see the error "SSL routines ... dh key too small"
If you see this error, then the server you are trying to connect to is using a certificate that does not meet modern cryptographic standards. Usually this means:

- The RSA and DHE keys are smaller than 2048 bits in length
- A signature algorithm weaker than SHA-256 is being used

The commands below can be used to lower the default OpenSSL security setting on Debian Linux, which would allow the connection to succeed and requirements above lifted.

```bash
# To view a list of all ciphers that will are consistent with the level 2 security setting (which will no longer now be required)
openssl ciphers -s -v 'ALL:@SECLEVEL=2'

# Lower the OpenSSL security setting from level 2 to level 1
sudo sed -i 's/CipherString = DEFAULT@SECLEVEL=2/CipherString = DEFAULT@SECLEVEL=1/' /etc/ssl/openssl.cnf
```

## On startup, I see "chown: changing ownership of '/home/node/postgresql': Operation not permitted"
If you see this error, it means that the container startup script was not able to set the appropriate permissions on the Stoplight data directory. The most common reason for this error is when the user ID that the in-container process is running as does not have permission to write to the mounted data directory.

To fix this issue, you'll need to know the path where you are storing Stoplight data. If you followed the [Docker Installation Guide](https://support.stoplight.io/hc/en-us/articles/360032728292), then you probably used a command similar to:

```bash
docker run ... -v $(pwd)/stoplight-data:/home/node/postgresql ...
```

This tells Docker to store Stoplight data in the current directory under a "stoplight-data" folder (ie, "./stoplight-data"). If you chose to store the data somewhere else, be sure to use that directory path instead.

To fix the permissions issues, you will need to change the ownership to a user with the ID of 101, which is the user ID of the container's "nginx" user:

```bash
chown -R 101:101 ./stoplight-data
```

Once the permissions are corrected, the Stoplight process should now be able to start correctly.

## When authenticating with LDAP I see the error "There were more entries matching the criteria..."
If you see the error below logged by the Stoplight API when authenticating with LDAP, then you may need to update your LDAP configuration's "base filter" attribute.

```bash
LDAP authentication failed: There were more entries matching the criteria contained in a 
```

SearchRequest operation than were allowed to be returned by the size limit configuration
Here is an example of a "base filter" that matches the user's "username" attribute with their LDAP user ID:

```bash
(uid={{username}})
```

Atlassian has a great article on writing LDAP filters available [here](https://confluence.atlassian.com/kb/how-to-write-ldap-search-filters-792496933.html) if you are unsure of what to use.