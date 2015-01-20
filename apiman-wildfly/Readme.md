# apiman Docker image

This is an example Dockerfile with [apiman on Wildfly](http://www.apiman.io/).

## Usage

    docker run -it jboss/apiman-wildfly

_NOTE_: This image provides a standalone wildfly profile for apiman. Currently, apiman does not support domain mode OOTB.

## Extending the image

    FROM jboss/apiman-wildfly
    # Do your stuff here
 
## Extending the image examples

To be able to create a management user to access the administration console create a Dockerfile with the following content

    FROM jboss/apiman-wildfly  
    RUN /opt/jboss/wildfly/bin/add-user.sh admin Admin#70365 --silent  
    CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0", "-c", "standalone-apiman.xml"]
 
Then you can build the image:

    docker build --tag=jboss/apiman-wildfly-admin .  
 
Run it:

    docker run -it -p 9990:9990 -p 8080:8080 jboss/apiman-wildfly-admin  
 
The administration console should be available at http://localhost:9990.
 
## Debug in a container

If you want to debug an application deployed in this apiman container, create a Dockerfile with the following content:

    FROM jboss/apiman-wildfly  
    RUN /opt/jboss/wildfly/bin/add-user.sh admin Admin#70365 --silent  
    # Default wildfly debug port  
    EXPOSE 8787  
    CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0", "-c", "standalone-apiman.xml", "--debug"]
 
 
Then you can build the image:

    docker build --tag=jboss/apiman-debug .  
 
Run it:

    docker run -it -p 8787:8787 -p 9990:9990 -p 8080:8080 jboss/apiman-debug

## Building on your own

You don't need to do this on your own, because we prepared an [automated build](https://registry.hub.docker.com/u/jboss/apiman-wildfly/) for this repository, but if you really want:

    docker build --tag=jboss/apiman-wildfly .

## Source

The source is [available on GitHub](https://github.com/jboss-dockerfiles/apiman).

## Version

Current/Latest apiman release is: 1.0.1.Final

## Issues

Please report any issues or file RFEs on [GitHub](https://github.com/jboss-dockerfiles/apiman/issues).
