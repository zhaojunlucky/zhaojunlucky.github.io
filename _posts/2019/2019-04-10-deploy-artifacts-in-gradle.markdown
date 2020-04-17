---
title: Deploy Artifacts in Gradle
date: 2019-04-10 14:38
categories:
- gradle
- artifacts
- deploy

---
Deploy Artifacts into a local path 

```groovy
// Add following task

uploadArchives {
    repositories {
        mavenDeployer {
            //mavenLocal()
            repository(url: 'file:///{local path}')
        }
    }
}

```