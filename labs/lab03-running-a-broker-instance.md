Lab 3. Running a Broker Instance
===
#### Run the broker in interactive mode
1. Once the broker is created, navigate to the `mybroker` instance `bin` folder
1. Run the `artemis` script to start the broker in interactive mode
```
$ ./artemis run
```
The broker will produce output similar to the following:
```
...
INFO  | main | Initialized dispatch-hawtio-console plugin
23:54:24,475 INFO  [org.apache.activemq.artemis] AMQ241001: HTTP Server started at http://localhost:8161
23:54:24,475 INFO  [org.apache.activemq.artemis] AMQ241002: Artemis Jolokia REST API available at http://localhost:8161/jolokia
```

#### Test the broker with the CLI
1. Navigate to the bin folder of the broker instance.
1. In a separate terminal/console run the artemis command to consume from the default address
```
$ ./artemis consumer
```
1. In another terminal/console do the same but this time to produce messages to the same default address
```
$ ./artemis producer
```
*You will see the producer sending 1000 messages, and the same amount, received by the consumer.*

#### Management console
1. To access the management web console, open a browser and goto http://localhost:8161/hawtio/login
1. Log in to the console using the username/password entered when the AMQ 7 instance was created.
 * In this case is `admin`/`admin`

#### Running as a Service (Optional)
If you want to run the broker in background as a system service you can use the provided script to archive it.

* For Linux/Unix
```
./artemis-service start
```
* For Windows
```
./artemis-service.exe start
```

*Remember to shut down the running instance before starting the service*

End of Lab 3.
