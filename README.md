# Elven systemd Tools

No matter how simple the commands, it is almost always worth taking a moment to create some bash scripts to automate the process. Here are three and half scripts that I find useful. They take a moment to setup, but they are very useful.

## modify-service-directory

This script can change the name of the directory in your service file. For instance, if you want to change references to **bcuser** to reference **ubuntu** then use these scripts. 

## Setup

Run the JsObjects script called **get-gist** from the root of your project. Choose **Elven systemd Node Tools**. Exit the script. A bunch of files should have been copied into your project.

In **setup-environment-service** modify these lines:

    export SYSTEMD_PROJECT_NAME=temp
    export SYSTEMD_DESCRIPTION="Temp Service"
    export SYSTEMD_PORT="SERVER_PORT=30026"

For instance:

    export SYSTEMD_PROJECT_NAME=my-project
    export SYSTEMD_DESCRIPTION="My Project Service"
    export SYSTEMD_PORT="SERVER_PORT=30027"

Now run:

    ./run-setup-service
    
That's all you need to do. Your project should now be running as a system service. Try to access it on the port you sepecified in **setup-environment-service**.

The sections below are provided as a reference. You don't need to do anything else.

## Modify package.json

This step and all subsequent steps are done automatically by **run-setup-service**. It is included only as a reference.

In **package.json** create a key value pair in the **Scripts** section called **start-service** that will start your service without relying on **nodemon** or other problematic services. The minimal possible entry would be:

    "start-service": "npm start",

Or maybe:

    "start-service": "node bin/www",

For instance:

```
"scripts": {
  "start": "nodemon ./bin/www",
  "start-service": "node bin/www",
  "build": "node_modules/.bin/webpack"
},    
```


## Source Setup Environment

This step is done automatically by **run-setup-service**. It is included only as a reference.

We need to **source** the file:

    source setup-environment-service

Run **setup-service**:

    ./setup-service

Your project might now be running as a service.

## setup-service

This script calls **mod-service**. If that call succeeds, it sets up your service.

Once you have set up your service, you can use these scripts to enable and start the service, or stop and disable the service.

## start-service

Start the service.

```bash
#!/bin/bash

sudo systemctl enable nrb.service
sudo systemctl start nrb.service
```

## stop-service

Stop the service.

```bash
#!/bin/bash

sudo systemctl stop nrb.service
sudo systemctl disable nrb.service
```
