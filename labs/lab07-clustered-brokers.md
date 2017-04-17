Lab 7. Clustered Brokers
===
#### Create a pair of brokers
1. In terminal 1 create `broker1`
```
$ <AMQ_HOME>/bin/artemis create --user admin --password password --role admin --allow-anonymous y --clustered --host 127.0.0.1 --cluster-user clusterUser --cluster-password clusterPassword --max-hops 1 <AMQ_HOME>/instances/broker1
```
1. In terminal 2 create `broker2`
```
$ <AMQ_HOME>/bin/artemis create  --user admin --password password --role admin --allow-anonymous y --clustered --host 127.0.0.1 --cluster-user clusterUser --cluster-password clusterPassword --max-hops 1 --port-offset 100 <AMQ_HOME>/instances/broker2
```
1. Start both brokers in each terminal/console

*Remember to allow traffic through the default ports. Check your firewall rules.*

After some initial negotiation you should see each broker log that a bridge has been created
```
19:44:21,792 INFO  [org.apache.activemq.artemis] AMQ241001: HTTP Server started at http://localhost:8161
19:44:21,798 INFO  [org.apache.activemq.artemis] AMQ241002: Artemis Jolokia REST API available at http://localhost:8161/jolokia
19:48:33,116 INFO  [org.apache.activemq.artemis.core.server] AMQ221027: Bridge ClusterConnectionBridge@7aea0d81 [name=$.artemis.internal.sf.my-cluster.0e3e3d97-1999-11e7-91bd-247703ddd1e0, queue=QueueImpl[name=$.artemis.internal.sf.my-cluster.0e3e3d97-1999-11e7-91bd-247703ddd1e0, postOffice=PostOfficeImpl [server=ActiveMQServerImpl::serverUUID=fe82ae53-1998-11e7-9bd2-247703ddd1e0], temp=false]@1bdbb549 targetConnector=ServerLocatorImpl (identity=(Cluster-connection-bridge::ClusterConnectionBridge@7aea0d81 [name=$.artemis.internal.sf.my-cluster.0e3e3d97-1999-11e7-91bd-247703ddd1e0, queue=QueueImpl[name=$.artemis.internal.sf.my-cluster.0e3e3d97-1999-11e7-91bd-247703ddd1e0, postOffice=PostOfficeImpl [server=ActiveMQServerImpl::serverUUID=fe82ae53-1998-11e7-9bd2-247703ddd1e0], temp=false]@1bdbb549 targetConnector=ServerLocatorImpl [initialConnectors=[TransportConfiguration(name=artemis, factory=org-apache-activemq-artemis-core-remoting-impl-netty-NettyConnectorFactory) ?port=61716&host=127-0-0-1], discoveryGroupConfiguration=null]]::ClusterConnectionImpl@1048855692[nodeUUID=fe82ae53-1998-11e7-9bd2-247703ddd1e0, connector=TransportConfiguration(name=artemis, factory=org-apache-activemq-artemis-core-remoting-impl-netty-NettyConnectorFactory) ?port=61616&host=127-0-0-1, address=, server=ActiveMQServerImpl::serverUUID=fe82ae53-1998-11e7-9bd2-247703ddd1e0])) [initialConnectors=[TransportConfiguration(name=artemis, factory=org-apache-activemq-artemis-core-remoting-impl-netty-NettyConnectorFactory) ?port=61716&host=127-0-0-1], discoveryGroupConfiguration=null]] is connected
```

End of Lab 7.
