This will house some information for operational support for the MSEL OA-PASS instance.

# Support Information
This is specific to the JHU Libraries implementation of PASS.  If we host other institutions' instances, this will probably be relevant to them as well.

## SSH Connection to the Environment
#### See a member of DRCC Operations if you don't already have a public key that's been uploaded to the Operations bastion server.

* Grab your favorite SSH client (Putty works as well, but command line OpenSSH clients are what is used and tested)
* ssh -l ${USERNAME} ops.pass.jhu.edu

##### Once on the server you have access to the following services

`ENVIRONMENT=(test|demo|prod)`

Service | Location
------- | --------
fcrepo | fcrepo-${ENVIRONMENT}.pass.local:8080
elasticsearch | elasticsearch-${ENVIRONMENT}.pass.cloud.library.jhu.edu:80

#### SSH Port Forwarding
Sometimes you just want to use your local workstation as a means of acheiving a goal.  With this, you can point your utilities to `localhost`
##### OpenSSH cli
* ssh -l ${USERNAME} -L${LOCALPORT}:${TARGET LOCATION} ops.pass.jhu.edu (ex. ssh -L8080:fcrepo-test.pass.local:8080)

This will bind your local port 8080 and tunnel this data over SSH to fcrepo-test.pass.local:8080.



### Tips for SSH (OpenSSH cli specific)
* Create a configuration file at ~/.ssh/config and set these values:
```
Host pass-test
    Hostname ops.pass.jhu.edu
    User ${USERNAME}
    IdentityFile ~/.ssh/pass.pem
    LocalForward 8080 fcrepo-test.pass.local:8080
    LocalForward 9090 elasticsearch-test.pass.cloud.library.jhu.edu:80
```
Now you can type `ssh pass-test` and it'll bind ports 8080 and 9090 and connect.

