---
sectionid: mongodb
sectionclass: h2
title: Deploy MongoDB
parent-id: lab-ratingapp
---

### Create MongoDB from template

{% collapsible %}
Red Hat OpenShift Service on AWS provides many container images and templates to make creating new applications & services easy. The template provides parameter fields to define all the mandatory environment variables (user, password, database name, etc) with predefined defaults including auto-generation of password values. It will also define both a deployment configuration and a service.

For this exercise we will use the following template:

* `mongodb-persistent` uses a persistent volume store for the database data which means the data will survive a pod restart. Using persistent volumes requires a persistent volume pool be defined in the Red Hat OpenShift Service on AWS deployment.

> **Hint** You can retrieve a list of templates using the command below. The templates are preinstalled in the `openshift` namespace.
> ```sh
> oc get templates -n openshift
> ```

Create a MongoDB deployment using the `mongodb-persistent` template. You're passing in the values to be replaced (username, password and database) which generates a YAML/JSON file. You then pipe it to the `oc create` command.

```sh
oc process openshift//mongodb-persistent \
    -p MONGODB_USER=ratingsuser \
    -p MONGODB_PASSWORD=ratingspassword \
    -p MONGODB_DATABASE=ratingsdb \
    -p MONGODB_ADMIN_PASSWORD=ratingspassword | oc create -f -
```

This is what you should see in your console:

![oc MongoDB](media/oc-mongodb.png)

If you now head back to the web console and make sure you are in the **workshop<student#>** project, you should see a new entry for MongoDB.

![MongoDB deployment](media/mongodb-overview.png)

{% endcollapsible %}

### Verify if the MongoDB pod was created successfully

{% collapsible %}

Run the `oc get all` command to view the status of the new application and verify if the deployment of the MongoDB template was successful.

```sh
oc get all
```

![oc get all](media/oc-status-mongodb.png)

{% endcollapsible %}

### Retrieve MongoDB service hostname

{% collapsible %}

Find the MongoDB service.

```sh
oc get svc mongodb
```

![oc get svc](media/oc-get-svc-mongo.png)

The service will be accessible at the following DNS name: `mongodb.workshop<student#>.svc.cluster.local` which is formed of `[service name].[project name].svc.cluster.local`. This resolves only within the cluster.

You can also retrieve this from the web console by toggling to the **Administrator** view, then navigating to **Networking -> Services** and selecting the mongodb service. You'll need this hostname to configure the `rating-api`.

![MongoDB service in the Web Console](media/mongo-svc-webconsole.png)

{% endcollapsible %}

> **Resources**
> * [OpenShift Documentation - Using images](https://docs.openshift.com/container-platform/latest/openshift_images/using_images/using-images-overview.html)
> * [OpenShift Documentation - Templates](https://docs.openshift.com/container-platform/latest/openshift_images/using-templates.html)
