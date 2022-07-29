# Fresh Install

### Steps to Add Sudo User on Ubuntu <a href="#ftoc-heading-1" id="ftoc-heading-1"></a>

#### Update Server packages <a href="#ftoc-heading-2" id="ftoc-heading-2"></a>

```
sudo apt update && sudo apt upgrade
```

Step 1: Create New User

1\. Log into the system with a **root** user or an account with **sudo** privileges.

2\. Open a terminal window and add a new user with the command:

```
adduser pbexpress
```

The **`adduser`** command creates a new user, plus a group and home directory for that user.

You may get an error message that you have insufficient privileges. (This typically only happens for non-root users.) Get around it by entering:

```
sudo adduser pbexpress
```

3\. You can replace **`newuser`** with any username you wish. The system will add the new user; then prompt you to enter a password. Enter a [great secure password](https://phoenixnap.com/blog/strong-great-password-ideas), then retype it to confirm.

4\. The system will prompt you to enter additional information about the user. This includes a name, phone numbers, etc. – these fields are optional, and can be skipped by pressing **Enter**.

![Creating a sudo user in Ubuntu](https://phoenixnap.com/kb/wp-content/uploads/2021/04/creating-sudo-user-ubuntu1.png)

#### Step 2: Add User to Sudo Group <a href="#ftoc-heading-3" id="ftoc-heading-3"></a>

Most Linux systems, including Ubuntu, have a user group for **sudo** users. To grant the new user elevated privileges, add them to the **sudo** group.

In a terminal, enter the command:

```
usermod -aG sudo pbexpress
```

Replace **`newuser`** with the username that you entered in Step 1.

Again, if you get an error, run the command with **sudo** as follows:

```
sudo usermod -aG sudo pbexpress
```

The **`-aG`** option tells the system to **append** the user to the specified **group**. (The **`-a`** option is only used with **`G`**.)

![Add user to sudo group ubuntu](https://phoenixnap.com/kb/wp-content/uploads/2021/04/creating-sudo-user-ubuntu2.png)

**Note:** Usermod command is a useful tool for user management. To learn more about its options, refer to our guide [How To Use The Usermod Command In Linux](https://phoenixnap.com/kb/usermod-linux).
