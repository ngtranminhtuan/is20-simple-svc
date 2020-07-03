# Create project
```
mvn archetype:generate -DarchetypeCatalog=https://maven.repository.redhat.com/ga/io/fabric8/archetypes/archetypes-catalog/2.2.195.redhat-000004/archetypes-catalog-2.2.195.redhat-000004-archetype-catalog.xml  \
 -DarchetypeGroupId=org.jboss.fuse.fis.archetypes  \
 -DarchetypeArtifactId=spring-boot-camel-xml-archetype  \
 -DarchetypeVersion=2.2.195.redhat-000004

```
# How to deploy on Openshift
Tweak the file openshift/solution.yml to enter your paramaters about the nexus mirror and git repository
```
oc cluster up
oc login -u system:admin
BASEURL=https://raw.githubusercontent.com/jboss-fuse/application-templates/GA
oc replace --force -n openshift -f ${BASEURL}/fis-image-streams.json
oc login -u developer
oc create -f ${BASEURL}/fis-image-streams.json
oc create -f openshift/solution.yml
oc new-app springboot-rest
```

# How to delete from Openshift

oc delete all -l component=springboot-rest



# Spring-Boot Camel QuickStart

This example demonstrates how you can use Apache Camel with Spring Boot
based on a [fabric8 Java base image](https://github.com/fabric8io/base-images#java-base-images).

The quickstart uses Spring Boot to configure a little application that includes a Camel
route that triggers a message every 5th second, and routes the message to a log.


### Building

The example can be built with

    mvn clean install


### Running the example locally

The example can be run locally using the following Maven goal:

    mvn spring-boot:run


### Running the example in Kubernetes

It is assumed a running Kubernetes platform is already running. If not you can find details how to [get started](http://fabric8.io/guide/getStarted/index.html).

Assuming your current shell is connected to Kubernetes or OpenShift so that you can type a command like

```
kubectl get pods
```

or for OpenShift

```
oc get pods
```

Then the following command will package your app and run it on Kubernetes:

```
mvn fabric8:run
```

To list all the running pods:

    oc get pods

Then find the name of the pod that runs this quickstart, and output the logs from the running pods with:

    oc logs <name of pod>

You can also use the [fabric8 developer console](http://fabric8.io/guide/console.html) to manage the running pods, and view logs and much more.


### More details

You can find more details about running this [quickstart](http://fabric8.io/guide/quickstarts/running.html) on the website. This also includes instructions how to change the Docker image user and registry.

