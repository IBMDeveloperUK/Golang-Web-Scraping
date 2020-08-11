# Lab 3 - Up in the :cloud:

In this lab you will deploy your application into a cloud environment. Because of its simplicity and ease, this lab will show you how to do this in IBM Cloud Foundry. 

Before you can complete any of the next steps, you must either [sign up](http://ibm.biz/golang_web) for an IBM Cloud account or make sure you are logged in to your existing account in a terminal.
If you have all of the tools installed then proceed to Step 2.

## IBM Cloud Foundry deployment

### Step 1

First you need to ensure you have installed the [ibmcloud cli tool](https://cloud.ibm.com/docs/cli?topic=cloud-cli-install-ibmcloud-cli#shell_install). If you haven't already done this, you can use do so with the following commands. With this you can access IBM Cloud from your command-line with the prefix `ibmcloud`.

Mac

```bash
curl -fsSL https://clis.cloud.ibm.com/install/osx | sh
```

Linux

```bash
curl -fsSL https://clis.cloud.ibm.com/install/linux | sh
```

Windows Powershell

```bash
iex(New-Object Net.WebClient).DownloadString('https://clis.cloud.ibm.com/install/powershell')
```

> **Note**: If you encounter errors like `The underlying connection was closed: An unexpected error occurred on a send`, make sure you have .Net Framework 4.5 or later installed. Also try to enable TLS 1.2 protocol by running the following command:

```bash
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```

Secondly, you will need to ensure you have got the Cloud Foundry CLI installed. If you haven't already got this, you can do so with the following command:

```bash
ibmcloud cf install
```

## Step 2

Now you need to prepare your application for Cloud Foundry. To do this, in the root directory of your project you will find a file called `manifest.yml`. This will be the building blocks for your application when pushing it up to the cloud. Inside this file add the following code. **Be sure to change/remove the commented code! (name & GO_INSTALL_PACKAGE_SPEC)**

```yaml
---
applications:
  - name: <name of your app as it will appear in IBM Cloud> (EXAMPLE = Web-Scraping-App)
    random-route: true
    memory: 128M
    env:
      GO_INSTALL_PACKAGE_SPEC: <path to your main.go file on your system> (EXAMPLE = github.com/golang-web-scraping)
```

## Step 3

In a terminal window, from within your project directory (`./go/src/github.com/<projectname>`), you are going to ensure you are logged in to your IBM Cloud account, target Cloud Foundry and then push your application up. To do this, follow the simple steps that follow:

1. Make sure you are logged into IBM Cloud via the CLI: `ibmcloud login`

> **Note**: If you have a federated ID, use `ibmcloud login --sso` to log in to the IBM Cloud CLI. Enter your user name, and use the provided URL in your CLI output to retrieve your one-time passcode. You know you have a federated ID when the login fails without the --sso and succeeds with the --sso option.

2. Enter your IBM Cloud credentials when prompted
3. Target Cloud Foundry with IBM Cloud by using: `ibmcloud target --cf`
4. Push your app into Cloud Foundry: `ibmcloud cf push`

**If you encounter an error with any of the commands above, please reach out to one of the mentors in the venue and we will assist you**

If the push is successful, your application will be created, and you should see the following output (or something very similar) :clap:

```bash
Waiting for app to start...

name:              Web-Scraping-App
requested state:   started
routes:            web-scraping-app-grouchy-klipspringer-in.eu-gb.mybluemix.net
last uploaded:     Thu 23 Jul 14:21:06 BST 2020
stack:             cflinuxfs3
buildpacks:        go

type:            web
instances:       1/1
memory usage:    128M
start command:   ./bin/web-scraping
     state     since                  cpu    memory      disk      details
#0   running   2020-07-23T13:21:20Z   0.0%   0 of 128M   0 of 1G     
```

To see your application running and have it output something to the screen, copy and paste the `routes` value from your terminal output into a browser address bar. 

Example: `web-scraping-app-persistent-hippopotamus.eu-gb.mybluemix.net`

The next stage of this workshop will be turning this simple web app into something that can scrape a web page, continue onto [Lab 4](./lab-4.md)