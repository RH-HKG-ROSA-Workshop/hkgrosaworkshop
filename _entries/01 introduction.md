---
sectionid: intro
sectionclass: h1
title: Red Hat OpenShift Workshop
type: nocount
is-parent: yes
---

[Red Hat OpenShift Service on AWS](https://aws.amazon.com/rosa/) (ROSA) is a fully managed Red Hat OpenShift service in AWS that is jointly engineered and supported by AWS and Red Hat. In this lab, you'll go through a set of tasks that will help you understand some of the concepts of deploying and securing container based applications on top of Red Hat OpenShift Service on AWS.

You can use this guide as an OpenShift tutorial and as study material to help you get started to learn OpenShift.

Some of the things you’ll be going through:

- Creating a [project](https://docs.openshift.com/container-platform/latest/applications/projects/working-with-projects.html) on the Red Hat OpenShift Service on AWS web console
- Deploying a MongoDB container that uses AWS Disks for [persistent storage](https://docs.openshift.com/rosa/storage/persistent_storage/osd-persistent-storage-aws.html)
- Restoring data into the MongoDB container by [executing commands](https://docs.openshift.com/container-platform/latest/nodes/containers/nodes-containers-remote-commands.html) on the Pod
- Deploying a Node JS API and frontend app from Git Hub using [Source-To-Image (S2I)](https://docs.openshift.com/container-platform/latest/openshift_images/using_images/using-s21-images.html)
- Exposing the web application frontend using [Routes](https://docs.openshift.com/container-platform/latest/networking/routes/route-configuration.html)
- Creating a [network policy](https://docs.openshift.com/container-platform/latest/networking/understanding-networking.html) to control communication between the different tiers in the application

You'll be doing the majority of the labs using the OpenShift CLI, but you can also accomplish them using the Red Hat OpenShift Service on AWS web console.
