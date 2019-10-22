# Introduction

JavaScript is one of the most widely used programming languages in web development without a doubt. There are bunch of web development frameworks and libraries available that speed up and simplify the development process. Vue.js is the rising star of front-end frameworks already used by world leading tech compnaies such as GitLab, Adobe, Alibaba where they build Single Page Applications and Progressive Web Application, etc.

# Learning Objective

This tutorial does not demonstrate fundamentals of Vue.js development. However, It does cover concepts such as creating, building, and deploying Vue.js projects. In this tutorial, you will learn how to:

* Create a Vue.js project by using Vue CLI
* Create a Toolchain on IBM Cloud
* Deploy static web application to Cloud Foundry

# Prerequisites

* Create a free [IBM Cloud account](https://cloud.ibm.com/)
* Install [Node.js](https://nodejs.org/en/download/) on your system
* Install [Vue CLI](https://cli.vuejs.org/guide/installation.html) on your system
* Install [Git](https://git-scm.com/downloads) on your system
* Create a [GitHub Account](https://cloud.ibm.com/)

# Featured Technologies

* [IBM Cloud](https://cloud.ibm.com) is a suite of cloud computing services from IBM that offers both platform as a service (PaaS) and infrastructure as a service (IaaS).
* [Node.js](https://nodejs.org/en/) is an open source, cross-platform runtime environment for developing server-side and networking applications.
* [Vue CLI](https://cli.vuejs.org) is a globally installed npm package and provides the vue command in your terminal.
* [Git](https://git-scm.com) is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.
* [GitHub](https://github.com) is a distributed version-control platform where users can collaborate on or adopt open source code projects, fork code, share ideas and more.
* [Cloud Foundry](https://www.ibm.com/cloud/cloud-foundry) is an open source, platform-as-a-service (PaaS) on IBM Cloud that enables you to deploy and scale apps without managing servers.

# Step 1. Create a Vue project

Make sure you have installed Vue CLI succesfully by running:

```bash
$ vue --version
```

Navigate to the directory where you want to store your project and create a new Vue project via command prompt.

```bash
$ vue create vue-tutorial
```

> Note: You can either select features by default with babel and eslint or manually with more configurations such as Router, Linter, Vuex, etc.

After project created successfully, as it mentioned in the command line, you can run the project with the following commands:

```bash
$ cd vue-tutorial
$ npm run serve
```

<p align="center"><img src="docs/screen1.gif"></p>

Open up your favorite browser and navigate to the URL where the app running at, in this case http://localhost:8080

<p align="center"><img src="docs/screen2.png"></p>

# Step 2. Commit your changes

You have genereted a boilerplate (aka template, skeleton) application and it is time to make changes according to your project idea. However, application development could be a long journey depending on the size of the project. You might forget what changes you have made or want to undo a feature. At this point, you need a Version Control System tool to keep track of project. In the rest of this tutorial, we will use Git and GitHub and if you are not familiar with these tools, you suggest you to go over [this](https://developer.ibm.com/tutorials/d-learn-workings-git/) tutorial.

Vue CLI initilizes git repository inside the project and makes the first commit by default which is a very cool feature.

Let's change the welcome message in the main page and make our second commit. For that, open the project with your preferred code editor and change the msg inside `<HelloWorld msg="Welcome to Your Vue.js App"/>` under the /src/App.vue folder.

> Note: If you did not stop serving process on the terminal, you can see the changes simultaneously. If you have already stoped the process, run `npm run serve` again in the project directory.

<p align="center"><img src="docs/screen3.gif"></p>

Return back to your existing CLI and stop development environment with `Ctrl + C` or open a new CLI window and change directory to your project.

```bash
$ git add .
$ git commit -m "my commit"
```

<p align="center"><img src="docs/screen4.gif"></p>

Yet, Git runs locally on a computer, isn't it better to host your repositories in a remote server and pretend from the computer crash. GitHub comes in play at this point. We will create a remote repository and push our local commits to GitHub servers.

In the next step, you will create a new repository on GitHub and add the URL for the remote repository where your local repository will be pushed. Finally, changes in your local repository will pushed up to the remote repository you specified as the origin.

<p align="center"><img src="docs/screen5.gif"></p>

<p align="center"><img src="docs/screen6.gif"></p>

# Step 3. Deploy your project to IBM Cloud

Nowadays, every developer has to have DevOps mindset to adjust fast and stable deployments of the applications. So that, this tutorial follows DevOps strategies to deploy your Vue project to IBM Cloud. IBM Cloud offers a service named Toolchain which is basically a set of tool integrations that support development, deployment, and operations tasks. There are a large number of toolchain templates depending on your intention, thought you will select the one for Cloud Foundry. Delivery Pipeline is an essential component of all the toolchain where the Build, Test, Release, and Deploy steps of Continious Integration and Continious Deployment handled.

<p align="center"><img src="docs/screen7.gif"></p>

>Note: You should select region, organization, and space correcly while creating Cloud Foundry applications. If you are not sure what are the correct values for these fields, you can learn by going to  **Manage > Account** and selecting **Account resources > Cloud Foundry orgs**.

Toolchain has been created succesfully, yet it fails to deploy because of incorrect configurations. So, it is time to fix the configurations in your Delivery Pipeline. Delivery Pipeline consist of two seperate stages, Build and Deploy.

Thus far, you have used `npm run serve` command while developing Vue project on your local system, however for production purposes your code must be builded. It is done via running `npm run build` command. Instead building the source code everytime on our development environment, you will set toolchain to do this in Build phase.

<p align="center"><img src="docs/screen8.gif"></p>

It is mentioned that the deployment will be on Cloud Foundry which is as Platform-as-a-Service (PaaS), that ensures the fastest, easiest, and most reliable deployment of cloud-native applications. You should create a file named *manifest.yml* where you set basic information about your application. 

```yaml
applications:
  - name: vue-tutorial
    path: ./dist
    buildpack: https://github.com/cloudfoundry/staticfile-buildpack.git
    random-route: true
    memory: 256M
    env:
      FORCE_HTTPS: true
```

> Note: You can find more information about attiributes in the following link: <https://docs.cloudfoundry.org/devguide/deploy-apps/manifest-attributes.html>

<p align="center"><img src="docs/screen9.gif"></p>

After adding *manifest.yml* file to your workspace, you will commit and push the changes to let local and remote repository to be noticed about the added file. Since changes in your GitHub repo triggers the pipeline, where Build and Deploy stages start doing their tasks in order, new process will start automatically. If you are fast enough to switch your screen to your browser, you can see your pipeline started doing its job.

This is what you expect to see when the CI/CD pipeline ends.

<p align="center"><img src="docs/screen10.png"></p>

# Step 4. Navigate to your project

Congratulations! You’ve successfully deployed your front-end application to IBM Cloud ! Now let's see how you can navigate to URL via browser.

<p align="center"><img src="docs/screen11.gif"></p>

Your toolchain has created a new Cloud Foundry application and assigned with a random URL. Finally, you have your application running in the cloud and ready to share with your friends and colleagues !!
