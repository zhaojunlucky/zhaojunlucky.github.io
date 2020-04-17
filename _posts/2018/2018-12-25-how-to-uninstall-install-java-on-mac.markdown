---
title: "How to Uninstall Install Java on Mac"
date: "2018-12-25 20:38"
categories: mac java jdk
---

After a new version Java released, the first thing for the Java developer is to upgrade to the latest version to have an experience of new features and improvements. Before to experience it, it needs to uninstall the previous installation first.

## How to uninstall Java on Mac
First thing is that we need to find where it's installed.
* Just run `/usr/libexec/java_home -v *10*`, it will show the Java install location.
  ```bash
  /Library/Java/JavaVirtualMachines/jdk-10.0.1.jdk/Contents/Home
  ```
* Then go to folder `/Library/Java/JavaVirtualMachines`, and remove `jdk-10.0.1.jdk` to uninstall jdk 10.
* And remove following folders
  ```bash
  sudo rm -rf "/Library/Internet Plug-Ins/JavaAppletPlugin.plugin"
  sudo rm -rf "/Library/PreferencePanes/JavaControlPanel.prefPane"
  ```

## How to install Java on Mac
Go to [https://www.oracle.com/technetwork/java/javase/downloads/index.html](https://www.oracle.com/technetwork/java/javase/downloads/index.html) to download Mac OS version Java and choose `dmg` file, then run it and follow the tutorial to install.

After the install done, run `java --version` to check the Java version.
