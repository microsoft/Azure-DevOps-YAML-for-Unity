---
page_type: sample
languages:
- yaml
products:
- dotnet
description: "A sample yaml configuration for creating a headless pipeline to build Unity3D projects for HoloLens2 with Azure Pipelines and Microsoft Hosted Agents."
urlFragment: "https://github.com/microsoft/Azure-DevOps-YAML-for-Unity "
---

# Azure DevOps YAML for Unity

<!-- 
Guidelines on README format: https://review.docs.microsoft.com/help/onboard/admin/samples/concepts/readme-template?branch=master

Guidance on onboarding samples to docs.microsoft.com/samples: https://review.docs.microsoft.com/help/onboard/admin/samples/process/onboarding?branch=master

Taxonomies for products and languages: https://review.docs.microsoft.com/new-hope/information-architecture/metadata/taxonomies?branch=master
-->

A sample yaml configuration for creating a headless pipeline to build Unity3D projects for HoloLens2 with Azure Pipelines and Microsoft Hosted Agents.

## Contents

Outline the file contents of the repository. It helps users navigate the codebase, build configuration and any related assets.

| File/folder       | Description                                |
|-------------------|--------------------------------------------|
| `azure-pipelines.yml`             | Sample source code.                        |
| `.gitignore`      | Define what to ignore at commit time.      |
| `CONTRIBUTING.md` | Guidelines for contributing to the sample. |
| `README.md`       | This README file.                          |
| `LICENSE`         | The license for the sample.                |

## Prerequisites

 - [x] **Azure DevOps** Organization/Tenant

 - [x] **Microsoft Account** or a work/organization account

 - [x] Knowledge how to add users to your Microsoft Azure Active Directory Tenant (if you plan to collaborate)

 - [x] Knowledge of how to ensure the **Mixed Reality Toolkit** (MRTK) foundation package is added to a Unity project *(**Release v2.1.0** at the time of this writing)*

 - [x] A **Unity 2019** *(2019.2.x at the time of this writing)* project with **MRTK Foundation added**

 - [x] A **Unity Plus/Pro license** serial key with at least 1 available seat to activate. 

## Setup


**If using Command Line for source control:**

- Git command line package for your platform installed
- The right Git Credential Manager or have configured SSH authentication

## Stand up a new Azure DevOps Environment

Navigate to https://dev.azure.com to sign in and create your project.

When you click the "+New project" button, you may choose your own name, description, visibility privacy (e.g. Public, Private, or Enterprise), version control (e.g. Git), and work item process (e.g. Agile).

## Install the extension ["Unity Tools for Azure DevOps"](https://dinomite-studios.github.io/unity-azure-pipelines-tasks/) 

Once you have your fresh work area created, please install the extension ["Unity Tools for Azure DevOps"](https://dinomite-studios.github.io/unity-azure-pipelines-tasks/) for use in your Azure DevOps organization. Instructions are available by following the link above.

The extension supports Microsoft Hosted Agents as well as Custom Agents.

***Note: A Unity Plus/Pro seat with at least one available activation is required to build using Hosted Agents,** which is what this document describes.*


## Clone your Azure DevOps  to your computer

Once you've got an Azure DevOps (ADO) project, click "Repos" to get started. You may follow the instructions at [docs.microsoft.com/](https://docs.microsoft.com/en-us/azure/devops/repos/git/clone?tabs=visual-studio&view=azure-devops#clone-a-repo) to see the many ways you can clone it to your computer. You can't clone a repo without a clone URL. 

### **Clone to your computer...**
If you are using the Command Line, pass this clone URL to ```git clone``` to make a local copy of the repo:

```git clone https://<org>@dev.azure.com/<org>/<proj>/_git/<proj>```

```git clone``` clones the repository from the URL in a folder under the current one.

### **...or push an existing repository from command line...**
If you are taking an existing Unity project (that must have a proper .gitignore in it), you may wish to [push it to Azure DevOps](https://docs.microsoft.com/en-us/vsts/git/tutorial/pushing?tabs=visual-studio):

``` git remote add origin https://<org>@dev.azure.com/<org>/<proj>/_git/<proj> ```

```git push -u origin --all ```

### **...or import a repository...**
There is an "Import" button that allows you to import another Git repository from a source control website, such as GitHub or ADO. Choose this if you already have a project repository elsewhere that you want to reference. Please ensure that it has a Unity-specific gitignore file in it.

### **...or initialize with a ReadMe or .gitignore**
You may choose to take this shortcut to initialize this repository with a .gitignore file and an optional ReadMe empty file. Note that once you click the "Initialize" button, your repo is no longer considered empty, and will now navigate you to the Files. 

Azure DevOps (and many other services) pull from GitHub's official ```gitignore``` list, if you wish to choose the [Unity.gitignore](https://github.com/github/gitignore/blob/master/Unity.gitignore). 

## Introduce a Unity Project
You will eventually need to tell an Azure Pipeline where to get source code for your Unity project. Please ensure that you have added a Unity-specific gitignore file to your ADO repo, and that you haven't already committed any files that need to be ignored during the cloning process. Your Unity project's Asset folder should become the ADO repository root. 

It is encouraged to stay up-to-date with the lastest software versions of Unity and Visual Studio, so we are going to proceed with **Unity 2019** *(2019.2.9f1 at the time of this writing)* and **Visual Studio 2019** *(16.3.6 at the time of this writing)* moving forward. 

*Older versions of Unity 2018 and Visual Studio 2017 are  supported, with some customization to the pipeline.*

Since we are adding tools to build & deploy Unity 3D projects designed for Windows 10 UWP apps, please configure the Unity project you want to work with to properly support Windows Mixed Reality,  Virtual Reality, spatial audio, XR settings, etc. by following the instructions here:
[How To Configure a New Unity Project for Windows Mixed Reality.](https://docs.microsoft.com/en-us/windows/mixed-reality/configure-unity-project) **The MRTK "Foundation" Unity Package must be imported into your Unity project, but the rest of it may be out-of-the-box empty and named anything.**

Additional Resources:

- [Windows Mixed Reality Development and Design Documentation](https://developer.microsoft.com/windows/mixed-reality)

- [Windows Mixed Reality Academy](https://docs.microsoft.com/en-us/windows/mixed-reality/tutorials)

Be sure to quit Unity to prepare for commiting to a git repository. If you have a proper .gitignore and haven't commited any files you don't need, then it should automatically ignore the directories such as Library, Temp, and Obj, the .csproj's, and almost everything else except the Assets and ProjectSettings directories. 

Once you add, commit, and push your Unity project files up to ADO, the only things you see in your repo's files should be Assets, Packages, ProjectSettings, and .gitignore.

## ♨ Get our ✨**Azure-Pipelines.yml**✨ Homemade Recipe! ♨
We have already done the hard work for you! We are providing you with an [Azure Pipelines YAML file](/azure-pipelines.yml) that will build your Unity project on a Windows Hosted Agent -- at no additional cost! 😉 

This build pipeline is designed for ARM UWP projects (what the HoloLens 2 uses), running Unity 2019.x, with MRTK Foundation. It is customizable to suit older versions of Unity, Visual Studio, and HoloLens 1. 

# 👉🏼[Download ```Azure-Pipelines.yml``` from this ReadMe.md👈🏼](/azure-pipelines.yml)

## Upload ```Azure-Pipelines.yml``` to your ADO Repo!
The easiest way to upload a file to ADO is to click the "Upload file(s)" button from your Repos page. Then you can simply drag and drop or browse for our ```azure-pipelines.yml``` file.

![Upload](/Images/upload.gif)

## Add your Secret Variables

This pipeline depends on Secret Variables that you must define within your Azure DevOps:
- [x] ```unity.username```  = Your Unity account email address
- [x] ```unity.password```  = Your Unity account password (keep it secret)
- [x] ```unity.serialkey``` = The serial key for your Unity Pro licence (keep it safe)

Without all three, this pipeline will fail to run. 🚫

![Secrets](/Images/secrets.gif)

Unity Pro will be licensed, utilized, and then unlicensed during the Unity and UnityTests jobs in this pipeline. A Unity Pro license works on 2 machines, and this pipeline should only use one licence at a time. However, should there be unexpected errors and deactivation doesn't complete properly, you may need to log into your Unity account and deactivate all. https://store.unity3d.com/account/licenses/other

## Create a new build pipeline
There are two ways to accomplish creating a new build pipeline in your ADO. In your Azure DevOps project, you may navigate to Pipelines by clicking "Set up build" (from the repo's files page) > "Existing Azure Pipelines YAML file."

![Build](/Images/build.gif)

Alternatively, click the "Pipelines" blue rocket icon > "New pipeline" button > "Azure Repos Git". 

![Pipeline](/Images/pipeline.gif)

Complete this step according to your needs.

# The YAML
Read the comments located [within the yml file](/azure-pipelines.yml) text for more information on how this pipeline works.