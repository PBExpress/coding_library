# Install Docker & Docker Compose (RHEL 8)

## Installing Docker CE and Docker compose on RHEL8 <a href="#ariaid-title1" id="ariaid-title1"></a>

RHEL8 does not support Docker CE by default. The following information provides a workaround to install compatible Docker CE on RHEL8.

### Install Docker CE and Docker compose on RHEL 8

To install Docker CE and Docker compose on RHEL 8:

1.  Add the external repository by running the following command.

    ```
    sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
    ```

    Verify whether the repository has been enabled. To do that, run the following command that returns detailed information about all the enabled repositories.

    ```
    sudo dnf repolist -v
    ```
2.  Install docker-ce with the --nobest option. With this option, the first version of `docker-ce` with satisfiable dependencies is selected as the "fallback" version.

    ```
    sudo dnf install --nobest docker-ce
    ```
3.  Install the latest available containerd.io package manually

    ```
    sudo dnf install https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.6-3.3.el7.x86_64.rpm
    ```
4.  Install the latest docker-ce version:

    ```
    sudo dnf install docker-ce
    ```
5.  Start and enable the docker daemon

    ```
    sudo systemctl enable --now docker
    ```

    Confirm whether the daemon is active by running this command:

    ```
    systemctl is-active docker
    ```
6.  Install docker-compose globally.

    Download the binary file from the project’s GitHub page:

    ```
    curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o docker-compose
    ```

    After the binary file is downloaded, move it to the /usr/local/bin folder, and then make it executable:

    ```
    sudo mv docker-compose /usr/local/bin && sudo chmod +x /usr/local/bin/docker-compose
    sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose 
    ```

For detailed information, see [https://linuxconfig.org/how-to-install-docker-in-rhel-8](https://linuxconfig.org/how-to-install-docker-in-rhel-8)

After this installation, you might encounter a Docker CE container connectivity issue. Complete these steps to resolve this issue.

### Resolve Docker CE container connectivity issue

To resolve Docker CE container connectivity issue:

1.  Check which interface Docker is using. For example, 'docker0'.

    ```
    ip link show
    ```
2.  Check available firewalld zones. For example, 'public'

    ```
    sudo firewall-cmd --get-active-zones
    ```
3.  Check which zone the Docker interface is bound to. Typically, the Docker interface is not bound to a zone yet.

    ```
    sudo firewall-cmd --get-zone-of-interface=docker0
    ```
4.  Add the 'docker0' interface to the 'public' zone. Changes are visible only after the firewalld is reloaded

    ```
    sudo nmcli connection modify docker0 connection.zone public
    ```
5.  Masquerading enables Docker ingress and egress.

    ```
    sudo firewall-cmd --zone=public --add-masquerade --permanent
    ```
6.  Reload the firewalld

    ```
    sudo firewall-cmd --reload
    ```
7.  Restart dockerd

    ```
    sudo systemctl restart docker
    ```
