Lab 5. Configuring a Topic
===
#### Creating a Topic using the CLI
1. Open the `etc/broker.xml` file with your favorite text editor.
1. Add a `multicast` type address with a topic
```
    <address name="testTopic">
        <multicast>
          <queue name="testTopic"/>
        </multicast>
    </address>
```
1. Start the broker or restart in case it’s already running.
1. Test the new created queue using running the following command in two (2) diferent terminal consoles
```
$ ./artemis consumer --destination topic://testTopic --message-count 10
```
1. Run the producer in a third terminal/console
```
$ ./artemis producer --destination topic://testTopic --message-count 10
```

End of Lab 5.
