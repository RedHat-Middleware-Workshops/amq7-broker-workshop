Lab 4. Configuring a Queue
===
#### Creating a Queue using the CLI
1. Open the `etc/broker.xml` file with your favorite text editor.
1. Add an `anycast` type address with a queue
```XML
    <address name="testQueue">
        <anycast>
          <queue name="testQueue"/>
        </anycast>
    </address>
```
1. Start the broker or restart in case it’s already running.
1. Test the new created queue using running the following command in two (2) diferent terminal consoles
```
$ ./artemis consumer --destination queue://testQueue --message-count 5
```
1. Run the producer in a third terminal/console
```
$ ./artemis producer --destination queue://testQueue --message-count 10
```

End of Lab 4.
