---
layout: default
title: How To - Upgrade EOL ubuntu distro to latest version 
---


# Intro
How to upgrade ubuntu from an EOL distro without formatting disk

# Steps to resolve 
Identify the upgrade path.  

For some reason mantic is in old-releases.ubuntu.com but sources are referring to archive.ubuntu.com
The upgrade path needed is:

  lunar  (old-ubuntu)   -> mantic (old-ubuntU-> noble (releases)    -> oracular (releases)

The UpgradeTool for mantic breaks because it can't find the repositories in archive. The only way this seems to be solvable is to upgrade from lunar to mantic manually, ie, change the apt sources.list to point to the mantic repositories in old-releases and run upgrade and dist-upgrade.  
Other third-party respositories and PPAs (usually sources.list.d) are best disabled for this process. 

Change the apt sources.list to point to the Mantic Minotaur repositories in old-releases.   
You can do this by editing the /etc/apt/sources.list file:  
```
sudo nano /etc/apt/sources.list
```

# Replace the existing jammy  repositories with the following:
```
deb http://old-releases.ubuntu.com/ubuntu/ mantic main restricted universe
deb http://old-releases.ubuntu.com/ubuntu/ mantic-updates main restricted universe
deb http://old-releases.ubuntu.com/ubuntu/ mantic-security main restricted universe
```
Update the package index 

```sudo apt update```  

Upgrade the system: 

```sudo apt full-upgrade``` or ```sudo apt upgrade ```  

Finally see if the automatic upgrade kicks in  
```sudo do-release-upgrade```


Finally for manual upgrade  you'd download the UpgradeTool from changelogs.ubuntu.com/meta-release and execute it,
https://old-releases.ubuntu.com/ubuntu/dists/mantic/main/dist-upgrader-all/current/
# Extract it into a new directory
```
mkdir upgrader  
tar -xaf mantic.tar.gz -C upgrader  
cd upgrader  
```
# Run the executable, the name changes based on the release
```sudo ./mantic --help```  

Use text mode installer mode  
```sudo ./mantic --frontend=DistUpgradeViewText```


### Ref: 
https://ubuntu.com/about/release-cycle
https://changelogs.ubuntu.com/meta-release
