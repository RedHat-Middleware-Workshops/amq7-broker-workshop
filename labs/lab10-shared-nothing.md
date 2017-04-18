Lab 10. Shared Nothing (replicated)
===
#### Create a high available broker with a shared nothing (replicated) using the CLI
1. Create a live broker
```
$ <AMQ_HOME>/bin/artemis create --replicated --failover-on-shutdown  --user admin --password password --role admin --allow-anonymous y --clustered --host 127.0.0.1 --cluster-user clusterUser --cluster-password clusterPassword  --max-hops 1 <AMQ_HOME>/instances/repLiveBroker
```
1. Create a backup broker
```
$ <AMQ_HOME>/bin/artemis create --replicated --failover-on-shutdown --slave --user admin --password password --role admin --allow-anonymous y --clustered --host 127.0.0.1 --cluster-user clusterUser --cluster-password clusterPassword  --max-hops 1 --port-offset 100 <AMQ_HOME>/instances/repBackupBroker
```
1. Add an `anycast` queue configuration to both brokers.
```XML
     <address name="haQueue">
        <anycast>
               <queue name="haQueue" />
        </anycast>
     </address>
```
1. Start the brokers, first the `repLiveBroker`, then the `repBackupBroker`

  *You should see the backup broker announce itself as a **backup** in the logs and the journal being replicated.*
```
...
22:31:05,221 INFO  [org.apache.activemq.artemis.core.server] AMQ221024: Backup server ActiveMQServerImpl::serverUUID=3fbf4e5d-19b0-11e7-ac4e-3c970e2638ff is synchronized with live-server.
22:31:05,449 INFO  [org.apache.activemq.artemis.core.server] AMQ221031: backup announced
```
1. Terminate the repLiveBroker

  *The `repBackupBroker` should start as live.*
```
...
22:32:54,018 INFO  [org.apache.activemq.artemis.core.server] AMQ221037: ActiveMQServerImpl::serverUUID=3fbf4e5d-19b0-11e7-ac4e-3c970e2638ff to become 'live'
```
1. Update the `repLiveBroker` configuration to check for a backup server that has failed over, so we don’t have an unaware live broker.
```XML
<ha-policy>
 <replication>
    <master>
       <check-for-live-server>true</check-for-live-server>
    </master>
 </replication>
</ha-policy>
```
1. Restart the repLiveBroker

 *You will see the live broker start and replicate back from the backup but notice it doesn’t start*
1. Manually terminate the `repBackupBroker` so the `repLiveBroker` takes over.

#### Automate the failover
1. Update the `repBackupBroker` configuration.
```XML
<ha-policy>
    <replication>
        <slave>
            <allow-failback>true</allow-failback>
        </slave>
    </replication>
</ha-policy>
```
1. Restart the `repBackupBroker` and wait for replication to start
1. Terminate the `repLiveBroker`
1. Restart the `repLiveBroker`
 *You will now see the live broker replicate back then take over as live*

#### Test failover queues
// TODO

End of Lab 10.
