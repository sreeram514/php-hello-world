# PHP source to image Helloworld Example

This is an example php application, which can be deployed to APPUiO using the following commands

## How to deploy

### Webconsole

* log into your OpenShift V3 Master 
* Create a new Project
* "Add to Project" a php:5.6 application
* name the application for example appuio-php-sti-example and provide the git repository URL, in this example https://github.com/appuio/php-helloworld.git
* the build and deployment is automatically triggered and the example application will be deployed soon

### CLI / oc Client

#### Create New OpenShift Project
```
$ oc new-project php-helloworld
```

#### Create Application and expose Service
```
$ oc new-app https://github.com/sreeram514/php-hello-world.git  --name=php-example

$ oc expose service php-example
```

## Add Webhook to trigger rebuilds

Take the Webhook GitHub URL from

```
$ oc describe bc appuio-php-sti-example

oc describe bc php-example
Name:			appuio-php-sti-example
Created:		20 seconds ago
Labels:			app=appuio-php-sti-example
Annotations:		openshift.io/generated-by=OpenShiftNewApp
Latest Version:		1
Strategy:		Source
Source Type:		Git
URL:			https://github.com/appuio/php-helloworld.git
From Image:		ImageStreamTag openshift/php:latest
Output to:		ImageStreamTag appuio-php-sti-example:latest
Triggered by:		Config, ImageChange
Webhook GitHub:		https://[Server]/oapi/v1/namespaces/php-helloworld/buildconfigs/appuio-php-sti-example/webhooks/[GitHubsecret]/github
Webhook Generic:	https://[Server]/oapi/v1/namespaces/php-helloworld/buildconfigs/appuio-php-sti-example/webhooks/[genericsecret]/generic
```

and add the URL as a Webhook in your github Repository, read https://developer.github.com/webhooks/ for more details about github Webhooks
