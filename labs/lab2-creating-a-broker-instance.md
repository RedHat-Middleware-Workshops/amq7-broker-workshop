Lab 2. Creating a Broker Instance
===

The `artemis` script located in the `bin` folder is the starting point to manage our AMQ installation.

#### Use the script to create a new broker instance

1. Execute the following command to create a new broker in the instances folder.
```
$ <AMQ_HOME>/bin/artemis create <AMQ_HOME>/instances/mybroker
```
1. The command will ask a series of questions in order to configure the broker instance:
 * Use `admin` as username and password for the mandatory user
 * Add the `admin` role to the admin user
 * Allow anonymous access by typing `Y` when asked

#### Directory Structure
```
$ cd instances/mybroker
$ tree
|-- bin
|-- data
|-- etc
|-- log
`-- tmp
```
| Folder | Description |
| ------ | ----------- |
| bin    | AMQ instance command line scripts to launch and manage |
| etc    | Broker instance configuration files |
| data   | Journal files storage for persistent messages |
| log    | Instance log files |
| tmp    | Temporary files |

End of Lab 2.
