# Elven systemd Tools

No matter how simple the commands, it is almost always worth taking a moment to create some bash scripts to automate the process. Here are three and half scripts that I find useful. They take a moment to setup, but they are very useful.

### modify-service-directory

This script can change the name of the directory in your service file. For instance, if you want to change references to **bcuser** to reference **ubuntu** then use this script. This script will be called automatically by **setup-service**.

```bash
#! /bin/bash

if [[ -z $1 ]]; then
    echo -e "You must pass in your home directory"
    echo -e "for instance:"
    echo -e "  ./modService bcuser"
    exit 1
fi

if [[ -z $2 ]]; then
    echo -e "You must pass in your service file name"
    echo -e "for instance:"
    echo -e "  ./modService bcuser eip.service"
    exit 1
fi


sed -i "s/home\/\([^/]*\)/home\/$1/g" $2
```

Modify the script to reference your service file.


### setup-service

This script calls **mod-service**. If that call succeeds, it sets up your service.

```bash
#! /bin/bash

function copyService() {
    ln -s $HOME/Git/writings/Tech/Markdown/ElvenImagePicker $HOME/bin/eip
    sudo cp -v eip.service /etc/systemd/system/.
    sudo systemctl enable SERVICE_FILE
    sudo systemctl start SERVICE_FILE
}

./mod-service $1 $2 && copyService
```

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
