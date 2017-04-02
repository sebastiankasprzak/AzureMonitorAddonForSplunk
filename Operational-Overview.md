The underlying mechanisms behind the operation of logs and metrics in Azure Monitor are fundamentally different. The information that goes into the log is at the whim of the resource. It's an all-or-nothing proposition when you ingest the log. Metrics, on the other hand, can be chosen at will by the consumer. So they'll be treated separately here. 

## Logs
The pipeline of a single log entry is simple: the resource generates the log entry, the log entry is dropped into an event hub (assuming you switched that on), the log entry sits time-ordered in the event hub for some retention period, a client (such as this add-on) retrieves logs by periodically reading new events in the event hub. The client may at any time go back in time to read older events by specifying a starting point in the hub. There may be multiple log categories for a resource and these align to multiple event hubs, each of which is subscribed to independently by a client.

The add-on is configured with the Event Hub Namespace, said namespace contains multiple hubs, each of which contains logs of a log category for a resource type. So, for example, all `Microsoft.Network/networkSecurityGroup` resources drop `NetworkSecurityGroupEvent` messages into a single event hub in the namespace. I am oversimplifying for clarity at this point.

Saving the details for later, the following must be in place to see logs appear in Splunk:  
* Configure each resource with event hub namespace  
* Configure the add-on to read logs from the event hub namespace

## Metrics
