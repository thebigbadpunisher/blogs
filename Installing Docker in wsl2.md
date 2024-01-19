Installing docker from main webpage using the convenience script :
```
 curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh ./get-docker.sh --dry-run
```

To create the `docker` group and add your user:

1.  Create the `docker` group.
    ```
    $ sudo groupadd docker
    ```

2.  Add your user to the `docker` group.    
    ```
    $ sudo usermod -aG docker $USER
    ```

3.  Log out and log back in so that your group membership is re-evaluated.
    > If you’re running Linux in a virtual machine, it may be necessary to restart the virtual machine for changes to take effect.

    You can also run the following command to activate the changes to groups:
    ```
    $ newgrp docker
	```

1.  Verify that you can run `docker` commands without `sudo`.
    ```
    $ docker run hello-world
    ```    
    This command downloads a test image and runs it in a container. When the container runs, it prints a message and exits.

    If you initially ran Docker CLI commands using `sudo` before adding your user to the `docker` group, you may see the following error:    
    ```none
    WARNING: Error loading config file: /home/user/.docker/config.json -
    stat /home/user/.docker/config.json: permission denied
    ```
    
    This error indicates that the permission settings for the `~/.docker/` directory are incorrect, due to having used the `sudo` command earlier.
    
    To fix this problem, either remove the `~/.docker/` directory (it’s recreated automatically, but any custom settings are lost), or change its ownership and permissions using the following commands:
    ```
    $ sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
    $ sudo chmod g+rwx "$HOME/.docker" -R
    ```
    

## Configure Docker to start on boot with systemd[](https://docs.docker.com/engine/install/linux-postinstall/#configure-docker-to-start-on-boot-with-systemd)

Many modern Linux distributions use [systemd](https://docs.docker.com/config/daemon/systemd/) to manage which services start when the system boots. On Debian and Ubuntu, the Docker service starts on boot by default. To automatically start Docker and containerd on boot for other Linux distributions using systemd, run the following commands:
```
$ sudo systemctl enable docker.service
$ sudo systemctl enable containerd.service
```

To stop this behavior, use `disable` instead.
```
$ sudo systemctl disable docker.service
$ sudo systemctl disable containerd.service
```

---
### ~/.profile content
	if grep -q "microsoft" /proc/version > /dev/null 2>&1; then
	    if ! service docker status > /dev/null 2>&1; then
	        sudo service docker start > /dev/null 2>&1
	    fi
	fi

Explanation:
1. sudo service docker start starts the Docker service with sudo privileges.
2. The ! negates the output of the command so that the following code block is only executed if the service is not running.
3. /dev/null 2>&1 redirects the output to null so that no output is displayed in the terminal.
--- 

### Running docker with sudo privileges without it asking for passwords everytime I log in:
Open the sudoers file with the command:
	`sudo visudo`

Add the following line to the end of the file:
	`yourusername ALL=(ALL) NOPASSWD: /usr/bin/dockerd`

Replace yourusername with your actual username.
This line allows your user to run the dockerd command as root without entering a password.
