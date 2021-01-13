# Lab 9. Shared Store

## Create a high available broker with a shared store using the CLI

1. Create a live broker

   ```sh
   $ <AMQ_HOME>/bin/artemis create --shared-store --failover-on-shutdown --data <AMQ_HOME>/instances/liveBroker/data --user admin --password password --role admin --allow-anonymous y --clustered --host 127.0.0.1 --cluster-user clusterUser --cluster-password clusterPassword --max-hops 1 <AMQ_HOME>/instances/liveBroker
   ```

1. Create a backup broker

   ```sh
   $ <AMQ_HOME>/bin/artemis create --shared-store --failover-on-shutdown --slave --data <AMQ_HOME>/instances/liveBroker/data --user admin --password password --role admin --allow-anonymous y --clustered --host 127.0.0.1 --cluster-user clusterUser --cluster-password clusterPassword --max-hops 1 --port-offset 100 <AMQ_HOME>/instances/backupBroker
   ```

1. Add an `anycast` queue configuration to both brokers.

   ```XML
     <address name="clusteredQueue">
        <anycast>
               <queue name="clusteredQueue" />
        </anycast>
     </address>
   ```

1. Start the brokers, first the `liveBroker`, then the `backupBroker`.

   >*You should see the backup broker announce itself as a **backup** in the logs.*

   ```sh
   ...
   21:46:08,600 INFO  [org.apache.activemq.artemis.core.server] AMQ221032: Waiting to become backup node
   21:46:08,605 INFO  [org.apache.activemq.artemis.core.server] AMQ221033: ** got backup lock
   …
   21:46:13,998 INFO [org.apache.activemq.artemis] AMQ241001: HTTP Server started at http://localhost:8261 21:46:14,001 INFO [org.apache.activemq.artemis] AMQ241002: Artemis Jolokia REST API available at http://localhost:8261/jolokia
   21:46:14,130 INFO  [org.apache.activemq.artemis.core.server] AMQ221031: backup announced
   ```

1. Terminate the `liveBroker`

   >*The `backupBroker` should start as live*

   ```sh
   ...
   21:57:55,926 INFO  [org.apache.activemq.artemis.core.server] AMQ221010: Backup Server is now live
   ```

1. Restart the `liveBroker`

   >*The `backupBroker` will automatically shutdown  and the `liveBroker` restart*

   ```sh
   ...
   22:01:51,764 INFO  [org.apache.activemq.artemis.core.server] AMQ221008: live server wants to restart, restarting server in backup
   ...
   ```

End of Lab 9.
