# Getting Started

Developing mods for Chivalry 2 has a few pre-requisites. After following this guide your PC will be ready to build Chivalry 2 mods.

## Index

* [Install git](#install-git)
* [Install UE 4.25](#install-ue-4.25)
* [Install the Compiler Toolset](#install-the-compiler-toolset)
* [Set up ArgonSDK](#set-up-argonsdk)

---

## Install git

Follow the official instructions from the [git documentation](https://git-scm.com/install/) to set up git.  If a prompt asks you to add `git` to the system PATH, select yes.

Validate that `git` is installed by opening up a command prompt, typing `git` and pressing enter.  If the installation failed, this will give you an error message saying something along the lines of "Command not found".

You may need to reboot to finalize installation. If you've run through the install and the command is still failing, try rebooting.

--- 

## Install UE 4.25

## Basic Installation 

If you're not planning on working with character models, armor, or other skeletal meshes (object models that aren't rigid/have bones), this basic installation step will work for you. Just be aware that you will not be able to build any custom skeletal meshes.

Follow the official instructions from the [Unreal Engine documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/install-unreal-engine) to set up UE 4.25. When you get to the section where you can select a version, select the latest 4.25 version (4.25.4).

## Advanced Installation

If you are planning on working with character models, armor, horses, or any other 3d models that have bones/joints/rigging, you will need UE 4.25+.  

Chivlary 2 was built with UE 4.25+, which contains a set of improvements and features backported from later versions of UE 4. There is no official build available for it, so you will have to build it from source.

!!! info
    This section still needs to be written. Feel free to reach out in the Chivalry 2 Discord, and we will help you out, and maybe write this tutorial section in the process.

---

## Install the compiler toolset

Follow the [official Unreal Engine instructions](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-visual-studio-code-for-unreal-engine#compilertoolsetforwindows) for installing the compiler toolchain.

--- 

## Set up ArgonSDK

Download the latest ArgonSDK.zip our [Google Drive](https://drive.google.com/drive/folders/1TgnTHGF9R13zBeEnN_XdR_LM1vmmQv7B).

Extract the ArgonSDK.zip to whereever you want to develop your mods. All of your mod development will take place in the location that you extract this to.

Open up a command prompt in the folder you extracted the SDK to

Run these commands to get the latest changes in the SDK:
```
git submodule update --init --recursive
git submodule update --recursive --remote
git pull
```

From here, you should be able to open the Unreal project called "TBL" and get started!
