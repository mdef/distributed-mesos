

# Apache Mesos redundant cluster.


The main focus to create reliable fully distributed self-sufficient multi master, multi  datacenter infrastructure without single point of failure and every component should run in container.


#####Overlay network between distributed nodes

Network connectivity candidats:
* [coreos/flannel](https://github.com/coreos/flannel "")
* [tinc-vpn](https://www.tinc-vpn.org/)

As we already used tinc for a while, we just extended tinc usage.

What the Tinc give us:
* If the node located in same network it will be available directly without any routing
* If the node located in another datacenter the tinc will automatically create a route  via one of the intermediate hops accessible by public ip.

We have a network layer we can run the base services.

#####We need distributed or immutable components:

* Multiple Zookeeper servers - for Mesos High-Availability Mode

* Multiple Apache Mesos masters - to control Mesos Agents and task execution.

* Multiple Apache slaves - to run the Applications.
* Multiple Mesosphere Marathon framework instances - to store Application definition and supply tasks to Apache master for distribution.

Core Application list running as Marathon application:
* Multiple mesosphere/mesos-dns - DNS is used to access Applications by dns name
* Multiple mesosphere/marathon-lb - used as load balancer and HAProxy - route by domain name functionality


#####The services provided by infrastructure above
* influxdb distributed metric storage (to be replaced as distributed functionality is not publicly available )
* telegraf node metrics collector stored in influxdb
* mariadb running in galera synchronous multi-master cluster mode - relational database
* grafana analytics and monitoring uses mariadb and influxdb
* minio running in distributed mode with erasure code  - S3 compatible storage


#Installation

We need to bootstrap the node, it is done by Ansible

It currently working on coreos, rancheros and any Linux box with SSH, Python and Docker installed. ( WIP: to run architecture agnostic aarch64 and armv7l )
