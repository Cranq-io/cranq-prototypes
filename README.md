# Introduction

Welcome to the public prototype repository for [Cranq](https://cranq.io)! This repository contains the official prototype set for CRANQ, developed & curated by us.

If you are looking for a general documentation of CRANQ, check out our dedicated [cranq-tutorials](https://github.com/Cranq-io/cranq-tutorials) repository!

# Structure

Upon the installation of the CRANQ IDE, this repository is copied to your home folder:
```
~/.cranq/repository
```
Every leaf directory in the folder structure represents a CRANQ prototype, structured by its ***namespace*** - for example, the description of the node ```data/array/Item deleter``` can be found under ```./data/array/item deleter```.

> **_How do I know the namespace of a node?_**
>
> The fully qualified name of a CRANQ node consists of its name, and its namespace path. Namespaces are divided by forward slashes ```/```, with the last segment being the node name.  
> For example:  
> ```data/array/Item deleter```  
> -> ```data```: root namespace  
> --> ```array```: sub-namespace  
> ---> ```Item deleter```: node name  


# Public namespaces

This repository contains the public namespaces. These root namespaces are reserved & maintained by the CRANQ development team.

> **_Caution_**
>
> These are maintained by the CRANQ IDE installer, any changes to them might get ***overwritten*** on upgrade or re-install:
> - Prototypes created in non-private namespaces
> - Changes to prototypes in non-private namespaces
> 
> For your own work, use ***Private namespaces*** instead.


# Private namespaces

By convention, private namespaces should follow the ```#{name}``` naming convention - these will be ignored during upgrade/install.
The installer will create a couple of these by default:
```
#team
#user
#workspace
```
Currently, any new node created through the CRANQ IDE will be automatically placed in the ```#workspace``` namespace. 

> **_How do I set/change the namespace of my node?_**
>
> Just rename your prototype in the CRANQ IDE, with the namespace path you wish to use:
> ```#user/custom/My prototype```  
> To create a new one, just rename your node with the namespace name you desire.

# Changing the location of private namespaces

By default, every namespace is created in the ``` ~/.cranq/repository``` folder. However, it is possible to map your own namespaces out to custom file system locations.

The CRANQ IDE maintains a configuration file, under ``` ~/.cranq/namespace-mapping.json```. By default, it looks something like this:

```json
{
    "": "<your_user_folder>\\.cranq\\repository",
    "#team": "<your_user_folder>\\.cranq\\repository\\#team",
    "#user": "<your_user_folder>\\.cranq\\repository\\#user",
    "#workspace": "<your_user_folder>\\.cranq\\repository\\#workspace"
}

```
You can use this file to change the folder location of your private namespaces.
- Use fully qualified paths for now
- Restart CRANQ for your changes to take effect
- You don't have to explicitly create a record here for all of your private namespaces - by default, everything is placed under ```""```, where the public ones are located
- Changing the path for ```""``` will change the default namespace path, but it is not recommeded at the moment

> **_Can I map my private namespaces to a git repository?_**
>
> Yes, absolutely! Just set your namespace path in this file to your locally cloned repository path, and you are set.


# Contributing to the public namespaces

Contributions to the public set of prototypes are welcome - if you have something to share, just drop us a line on [Discord](https://discord.gg/UgsjNtZW65)!
