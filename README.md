# node-tools.elvenware.com

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

sed -i "s/home\/\([^/]*\)/home\/$1/g" eip.service
```

### setup-service

This script calls **mod-service**. If that call succeeds, it sets up your service.

```bash
#! /bin/bash

function copyService() {
    ln -s $HOME/Git/writings/Tech/Markdown/ElvenImagePicker $HOME/bin/eip
    sudo cp -v eip.service /etc/systemd/system/.
    sudo systemctl enable eip.service
    sudo systemctl start eip.service
}

./mod-service $1 && copyService
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
