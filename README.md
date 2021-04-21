Ruby Sample App on OpenShift
Installation
Debugging Unexpected Failures
Adding Webhooks and Making Code Changes
License
Ruby Sample App on OpenShift
This is a basic ruby application for OpenShift v3 that you can use as a starting point to develop your own application and deploy it on an OpenShift cluster.

If you'd like to install it, follow these directions.

The steps in this document assume that you have access to an OpenShift deployment that you can deploy applications on.

Installation
These steps assume your OpenShift deployment has the default set of ImageStreams defined. Instructions for installing the default ImageStreams are available here. If you are defining the set of ImageStreams now, remember to pass in the proper cluster-admin credentials and to create the ImageStreams in the 'openshift' namespace.

Fork a copy of ruby-ex

Add a Ruby application from your new repository:

 $ oc new-app openshift/ruby:25~https://github.com/< yourusername >/ruby-ex 
A build should start immediately. To run another build, run:

 $ oc start-build ruby-ex
Once the build is running, watch your build progress:

 $ oc logs build/ruby-ex-1
Wait for ruby-ex pods to start up (this can take a few minutes):

 $ oc get pods -w
Sample output:

 NAME               READY     STATUS       RESTARTS   AGE
 ruby-ex-1-build    0/1       ExitCode:0   0          2m
 ruby-ex-1-deploy   1/1       Running      0          25s
 ruby-ex-1-hrek2    1/1       Running      0          17s
Check the IP and port the ruby-ex service is running on:

 $ oc get svc
Sample output:

 NAME      CLUSTER_IP      EXTERNAL_IP   PORT(S)    SELECTOR                   AGE
 ruby-ex   172.30.97.209   <none>        8080/TCP   deploymentconfig=ruby-ex   2m
In this case, the IP for ruby-ex is 172.30.97.209 and it is on port 8080.
Note: you can also get this information from the web console.

Debugging Unexpected Failures
Review some of the common tips and suggestions here.

Adding Webhooks and Making Code Changes
Since OpenShift V3 does not provide a git repository out of the box, you can configure your github repository to make a webhook call whenever you push your code.

From the console navigate to your project.
Click on Browse > Builds
From the view for your Build click on the link to display your GitHub webhook and copy the url.
Navigate to your repository on GitHub and click on repository settings > webhooks
Paste your copied webhook url provided by OpenShift
Change the Content type to application/json - Thats it!
After you save your webhook, if you refresh your settings page you can see the status of the ping that Github sent to OpenShift to verify it can reach the server.
