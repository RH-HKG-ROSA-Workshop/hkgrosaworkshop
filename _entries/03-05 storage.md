---
sectionid: lab2-storage
sectionclass: h2
title: Persistent Storage
parent-id: lab-clusterapp
---

In this section we will execute a simple example of using persistent storage by creating a file that will be stored on a persistent volume in our cluster and then confirm that it will "persist" across pod failures and recreation.

{% collapsible %}

Inside the OpenShift web UI click on **Storage -> PersistentVolumeClaims** in the left menu. You will then see a list of all persistent volume claims that our application has made.  In this case there is just one called "ostoy-pvc".  You will also see other pertinent information such as whether it is bound or not, size, and storage class.

![StoragePVC](media/managedlab/17-1-ostoy-storagepvc.png)

If you drill into **ostoy-pvc**, you will see *ReadWriteOnce* under *Access Modes*, which means that the volume can only be mounted to one node but the pod(s) can both read and write to that volume.  The default in ROSA is for Persistent Volumes to be backed by the Amazon Web Services Elastic File System (AWS EFS) Disk, but it is possible to use AWS Elastic Block Store (AWS EBS).  ([See here for more info on AWS EBS](https://docs.openshift.com/container-platform/latest/storage/persistent_storage/persistent-storage-aws.html))

In the OSToy app click on *Persistent Storage* in the left menu.  In the "Filename" area enter a filename for the file you will create. (ie: "test-pv.txt")

Underneath that, in the "File Contents" box, enter text to be stored in the file. (i.e. "ROSA is the greatest thing since sliced bread!" or "test" :) ).  Then click "Create file".

![Create File](media/managedlab/17-2-ostoy-createfile.png)

You will then see the file you created appear above under "Existing files".  Click on the file and you will see the filename and the contents you entered.

![View File](media/managedlab/18-ostoy-viewfile.png)

We now want to kill the pod and ensure that the new pod that spins up will be able to see the file we created. Exactly like we did in the previous section. Click on *Home* in the left menu.

Click on the "Crash pod" button.  (You can enter a message if you'd like).

Click on *Persistent Storage* in the left menu

You will see the file you created is still there and you can open it to view its contents to confirm.

![Crash Message](media/managedlab/19-ostoy-existingfile.png)

Now let's confirm that it's actually there by using the CLI and checking if it is available to the container.  If you remember we mounted the directory `/var/demo_files` to our PVC.  So get the name of your frontend pod

`oc get pods`

then get an SSH session into the container

`oc rsh <podname>`

then `cd /var/demo_files`

if you enter `ls` you can see all the files you created.  Next, let's open the file we created and see the contents

`cat test-pv.txt`

You should see the text you entered in the UI.

```
$ oc get pods
NAME                                  READY     STATUS    RESTARTS   AGE
ostoy-frontend-5fc8d486dc-wsw24       1/1       Running   0          18m
ostoy-microservice-6cf764974f-hx4qm   1/1       Running   0          18m

$ oc rsh ostoy-frontend-5fc8d486dc-wsw24
/ $ cd /var/demo_files/

/var/demo_files $ ls
lost+found   test-pv.txt

/var/demo_files $ cat test-pv.txt 
ROSA is the greatest thing since sliced bread!
```

Then exit the SSH session by typing `exit`. You will then be in your CLI.

{% endcollapsible %}
