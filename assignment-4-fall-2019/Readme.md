# Assignment-4: Distributed Monitoring


**Due: 1 Week**

10/10/2019

# Context

The goal of this assignment is to get you familiar with collectd, influxdb, grafana and the idea of using heartbeats (watchdogs) for monitoring distributed applications. In this assignment you will implement a subscriber with a heartbeat monitor that receives messages from multiple publishers and then periodically insert the results into a time-series database (influx db). Influx db allows use of java script user interfaces to create dashboards (see influx db tutorial). The data entering Influx db could be graphically visualized using a tool called grafana.

Collectd is used to collect performance metrics from the computing machines.

# Tasks

* Create 2 AWS instances within a security group that allows all traffic to that security group on all protocols. https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html
* Ensure all three instances are associated to this security group.
* Allocate  elastic IP with these two instances. https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html. 
* Install collectd on both these machines.
* Install influx-db on one of these machines.
* Configure the collect-d on these two machines to talk to the influx-db server. Look at https://anomaly.io/collectd-metrics-to-influxdb/index.html
* Then, implement two publishers (on the first machine where influx is not running) that reads the provided csv file and publishes sensor data at regular intervals (note that you can use either MQTT or ZeroMQ. If you use zeroMQ then you need to create a broker of your own. it should loop the file as required.  You can use the test mosquitto service https://test.mosquitto.org/), a broker to relay the data, and a subscriber to receive the data from the publishers.
*  Design a heartbeat monitor (run on same machine as the publishers) in the subscriber which keeps a track if both the publishers are alive or not. i.e the subscriber has to maintain a record of the message timestamps from both the publishers, and if it does not receive message from a publisher for a preset threshold of time (say 50 seconds) then you need to check the status (using pid) of publisher process and decide if the publisher is alive or not.  
* Show through scenarios each to show 1) Both publishers working. 2) One publisher not working. and 3) Both publishers are not alive. 
* Update the Subscriber script to accommodate Influx db and write all the sensor data being received and the heartbeat messages onto the database.
* plot the time series data being received by server using grafana.  (note that you should run grafana on your VM and connect to the influx db using the elastic ip.).   Configure grafana to automatically update every 5s.



**Submissions**

+   The scripts for the entire assignment. (Comments are mandatory)
+   Screenshots (jpg images) of the grafana plots.
+  influxdb export as csv (https://community.influxdata.com/t/export-daily-data-to-csv/2217) 
+   Answers to all the questions asked above (add it as a markdown file)
+   A readme file (markdown) with a brief architecture, a few words about the
    assignment, and testing instructions.


**Note** - Make sure all your instances are stopped after you finish the assignment. Delete your elastic ip from the instances after the experiment. 



**Note**
-   Use Ubuntu 18.04 and Python 3 for this assignment.

**References**

-    [ZMQ Examples](https://github.com/vu-resilient-distributed-systems/lectures-fall-2019/tree/master/Module-2-MiddlewareAndBackend/examples/ZMQ)
-   [Influx db set up and update example.](https://github.com/vu-resilient-distributed-systems/lectures-fall-2019/tree/master/Module-4-Finding-Failures/examples/InfluxDB)
-   [**http://docs.grafana.org/guides/getting\_started/**](http://docs.grafana.org/guides/getting_started/)
    (getting started with grafana)

