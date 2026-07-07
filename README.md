# Introduction 
This repository demonstrates the possibility to combine Microsoft Power Platform with Azure DevOps. In this scenario, Azure DevOps is used as the central orchestration
tool for code versioning, solution deployment using CI/CD pipelines. It has the potential to enhance Application Lifecycle Management for Power Platform solutions.

# Getting Started
## 1. Prerequisities

In oder to enable this possiblity, a few things need to be prepared beforehand:
  1. Install the **Power Platform Build Tool** through marketplace on DevOps within your organizaion. 
  2. Create one or more **App Registration** with the **"Dynamics Lifecycle services - user impersonation"** permission.
  3. Create **service connections** in DevOps using the App Reg for authentication (at least 2 service connections are needed, 
     one points to the dev environment and one points to the target prod environment. 3 service connections are required, if the dev-test-prod path is standard.).
  4. Create a **repository** for your Power Platform project.
  5. Add the App Reg (service principal) as **Application user** into proper power platform environments (dev-test-prod) respectively.
     1. Go to **Power Platform Admin Center** --> **Environments**
     2. Select the **target environment** (dev, test, pord)
     3. Go to **settings** --> **Application User**
     4. Click **New App user** --> search for the **App registration** created in Previous step --> Add it and provide it with either **System Customizer** or **System Administrator** role.
     5. Repeat the steps above for all related environments.

## 2. CI/CD Pipelines

Using the azure-pipeline.yml file for updating the code base from the development environment, and also for deployment solution to the 
target (test or production) environment. The pipeline is designed for both updating/synchronization and deployment using different stages, select the appropriate stage(s) while triggering the pipeline.

**Note:** the build service account "{YourProjectName} Build Service ({YourOrgName})" need to be granted with the git **"contributer"** permission on the repository scope, since the build service account is used to upload changes to the remote repo branch. The exact permissions required are as follows:

|Permission |	Setting |
|-----------|-----------|
| Contribute |	Allow |
|  Read	   |    Allow |
|Create branch |	Allow (recommended)| 
|Create tag |	Allow (if pushing tags)| 

## 🤝 Contributing
1. Fork → dev branch
2. uv sync → test

License: MIT | ⭐ Star if useful!

Built May 2026

