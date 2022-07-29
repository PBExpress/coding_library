# Log into WSL as Root

First, close the Ubuntu console prompt for the normal user.

Then open Windows command prompt by clicking the start button and finding Commend Prompt or searching for it as shown in the image below.

![windows command prompt](https://websiteforstudents.com/wp-content/uploads/2021/04/windows-command-prompt.webp)

When the command Prompt opens, type the commands below to configure Ubuntu WSL app to login as root instead of a normal user account.

![ubuntu start wsl as root](https://websiteforstudents.com/wp-content/uploads/2021/06/ubuntu-start-wsl-as-root.webp)

**Ubuntu:**

```
ubuntu config --default-user root
```

**Ubuntu 20.04:**

```
ubuntu2004 config --default-user root
```

**Ubuntu 18.04:**

```
ubuntu1804 config --default-user root
```

After running the command above for the respective Ubuntu version, go and start up Ubuntu WSL app and this time the root account should be logged in.
