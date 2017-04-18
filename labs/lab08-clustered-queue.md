Lab 8. Clustered Queue
===
#### Create a clustered queue
To have a clustered queue it must be defined in both brokers.
1. Add an anycast queue configuration to both brokers.
```XML
     <address name="clusteredQueue">
        <anycast>
               <queue name="clusteredQueue" />
        </anycast>
     </address>
```
1. Restart the brokers

#### Run a consumer connected to each broker
1. In `broker1`
```
$ ./artemis consumer --message-count 5 --destination queue://clusteredQueue
```
1. In `broker2`
```
$ ./artemis consumer --message-count 5 --url tcp://localhost:61716 --destination queue://clusteredQueue
```
1. Now run the producer connected to `broker1` and send 10 messages
```
$ ./artemis producer --message-count 10 --destination queue://clusteredQueue
```
*You will see each consumer receives 5 messages in a round robin fashion*

#### Run a disconnected consumer
1. Now run the producer first again
```
$ ./artemis producer --message-count 10 --destination queue://clusteredQueue
```
1. Run the broker2 consumer first
```
$ ./artemis consumer --message-count 10 --url tcp://localhost:61716 --destination queue://clusteredQueue
```
1. Run the broker1 consumer next
```
$ ./artemis consumer --message-count 10 --destination queue://clusteredQueue
```
*You will see that only 1 consumer received the messages as they were load balanced on demand*

#### Message load balancing strategy
1. Update the load balancing to strict in the `etc/broker.xml` file
```XML
  <cluster-connections>
         <cluster-connection name="my-cluster">
            <connector-ref>artemis</connector-ref>
            <message-load-balancing>STRICT</message-load-balancing>
            <max-hops>1</max-hops>
            <discovery-group-ref discovery-group-name="dg-group1"/>
         </cluster-connection>
  </cluster-connections>
```
1. Restart the brokers and run again the previous exercise

  *You will notice that both the consumers receive messages even when disconnected*

End of Lab 8.
