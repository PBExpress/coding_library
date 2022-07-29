# Node JS (NPM)

In this guide, we’ll show you how to install Node.js on Ubuntu 20.04 LTS. We need to add Node.js PPA to your Ubuntu 20.04 LTS, 18.04 LTS, 16.04 LTS systems and install it. Latest version of [Node.js ppa](https://github.com/nodesource/distributions) is maintaining by its official website on Github. Node.js is one of the most popular web technologies to build network applications quickly.

Same instructions you can apply for any Debian based distribution, including Kubuntu, Linux Mint and Elementary OS.

[Node.js](https://nodejs.org/en/) is an open-source and cross-platform compatible technology. Node.js is used by many developers to increase the functionality of a web application. The primary benefit is Node.js is a server-side execution that allows JavaScript to run without the client.

### Install Node.js on Ubuntu 20.04 with PPA <a href="#install" id="install"></a>

There are several ways to install Node.js. However, we will show you the two simplest and most efficient way to install Node.js. Also, you can download the Node.js latest version via .rpm, .deb and Snap packages.

### 1. Add Node.js from NodeSource

This is the simplest method to install a specific version of Node.js. You can quickly follow the below steps to install Node.js 15.x, 14.x, 13.x version. To install Node.js and npm from the NodeSource repository, follow the below steps:

**Current Release**

Currently Node.js v15.x is latest release available. First, add the latest Node.js PPA to your system to install Nodejs on Ubuntu.

```bash
curl -sL https://deb.nodesource.com/setup_current.x | sudo -E bash -
```

**LTS Release (Recommended)**

Currently Node.js v14.x is stable LTS release available. First, add the latest Node.js PPA to your system to install Nodejs on Ubuntu.

```bash
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
```

If you need to install any other previous version, change the version number. For example `13.x`, `12.x`.

### 2. Install Node.js on Ubuntu 20.04

Once the Node.js PPA is enabled, install Node.js using apt-get command. This will also install [NPM](https://www.npmjs.com/package/npm) with Node.js. Also, it will install the many other dependent packages on your systems.

```bash
sudo apt-get install -y nodejs
```

### 3. Check Installed Node.js and NPM version

Finally, Node.js and NPM successfully installed in your system. You can check and verify the installed Node.js version using the following command.

```bash
node --version
```
