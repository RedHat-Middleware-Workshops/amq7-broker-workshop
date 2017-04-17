Lab 1. Installation
===

#### Download zip file from Red Hat Customer Portal
1. Open a browser to log in to the portal at  https://access.redhat.com/downloads
1. Select product: Red Hat JBoss AMQ in the product downloads list
1. Select version: 7.0.0 from drop-down menu
1. In the releases tab click on Red Hat JBoss A-MQ 7.0.0 Broker download link

#### Install the software by unzipping the file into the designated workshop path (/home/user/workshop-amq)

```
$ unzip jboss-amq-7.x.x.zip
```

*The directory created by extracting the archive will be referenced now on as **AMQ_HOME***

#### Directory Structure

```
$ tree
|-- bin
|-- etc
|-- examples
|-- lib
|-- schema
`-- web
```

| Folder | Description |
| ------ | ----------- |
| bin    | AMQ scripts and native journal lib |
| etc    | Red Hat branding and extra configuration |
| examples | Full set of runnable JMS and Java EE examples |
| lib    | The AMQ 7 runtime jars and libraries |
| schema | XML Schema to validate the JBoss AMQ configuration files |
| web    | Web loaded with hawt.io console, jolokia |

End of Lab 1.
