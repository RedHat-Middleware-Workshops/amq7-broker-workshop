# Lab 1. Installation

## Download zip file from Red Hat Customer Portal

1. Open a browser to log in to the Red Hat developer portal at  https://developers.redhat.com/products/amq/download

1. Scroll down to the **All Downloads** section

1. Find the **GA December 2020** group

1. In the table click on the **AMQ Broker** button to download [Red Hat AMQ Broker 7.8.0](https://developers.redhat.com/download-manager/file/amq-broker-7.8.0-bin.zip)

   > You will need to login into the portal using your Red Hat developer or customer account.

## Install the software by unzipping the file into the designated workshop path ($HOME/workshop-amq)

```sh
$ unzip amq-broker-1.8.0-bin.zip
```

> The directory created by extracting the archive will be referenced now on as **AMQ_HOME**

## Directory Structure

```sh
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
| schema | XML Schema to validate the AMQ configuration files |
| web    | Web loaded with hawt.io console, jolokia |

End of Lab 1.
