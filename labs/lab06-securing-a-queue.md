Lab 6. Securing a Queue
===
#### Adding security to a Queue
1. Add a new user `myuser` to the broker instance
```
$ ./artemis user add --user myuser --password mypassword --role mygroup
```
1. Update the security settings to only allow **send** to the new user’s role `mygroup`.
```XML
  <security-settings>
         <security-setting match="#">
        ...
            <permission type="consume" roles="admin"/>
            <permission type="browse" roles="admin"/>
            <permission type="send" roles="admin,mygroup"/>
            <!-- we need this otherwise ./artemis data imp wouldn't work -->
            <permission type="manage" roles="admin"/>
         </security-setting>
  </security-settings>
```

#### Testing the Security Settings
1. Test sending messages to the previously created topic testTopic
```
$ ./artemis producer --destination topic://testTopic --message-count 10 --user myuser --password mypassword
```
1. Test consuming messages from the same topic using the new user.
```
$ ./artemis consumer --destination topic://testTopic --message-count 10 --user myuser --password mypassword
```
You will get an ActiveMQSecurityException
```
javax.jms.JMSSecurityException: AMQ119032: User: myuser does not have permission='CREATE_NON_DURABLE_QUEUE' on address testTopic
    at org.apache.activemq.artemis.core.protocol.core.impl.ChannelImpl.sendBlocking(ChannelImpl.java:409)
    at org.apache.activemq.artemis.core.protocol.core.impl.ChannelImpl.sendBlocking(ChannelImpl.java:320)
    at org.apache.activemq.artemis.core.protocol.core.impl.ActiveMQSessionContext.createQueue(ActiveMQSessionContext.java:634)
    at org.apache.activemq.artemis.core.client.impl.ClientSessionImpl.internalCreateQueue(ClientSessionImpl.java:1836)
    at org.apache.activemq.artemis.core.client.impl.ClientSessionImpl.createTemporaryQueue(ClientSessionImpl.java:429)
    at org.apache.activemq.artemis.jms.client.ActiveMQSession.createConsumer(ActiveMQSession.java:690)
    at org.apache.activemq.artemis.jms.client.ActiveMQSession.createConsumer(ActiveMQSession.java:359)
    at org.apache.activemq.artemis.jms.client.ActiveMQSession.createConsumer(ActiveMQSession.java:331)
    at org.apache.activemq.artemis.cli.commands.util.ConsumerThread.consume(ConsumerThread.java:146)
    at org.apache.activemq.artemis.cli.commands.util.ConsumerThread.run(ConsumerThread.java:64)
Caused by: ActiveMQSecurityException[errorType=SECURITY_EXCEPTION message=AMQ119032: User: myuser does not have permission='CREATE_NON_DURABLE_QUEUE' on address testTopic]
    ... 10 more
```

End of Lab 6.
