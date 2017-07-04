Zeppelin and Flink in Docker
===============

This is a Docker image appropriate for running a special version of Apache Zeppelin forked by [Radicalbit](https://github.com/radicalbit/) and linked with Apache Flink. 
Radicalbit improved Apache Zeppelin in order to ease Streaming developement using features of Apache Flink that is the most important real streaming engine.
You can run it locally with docker-compose in which case you get four containers by default:
* `zeppelin` - runs Zeppelin version forked by Radicalbit inserting one specific example of streaming flink job.
* `flink-jobmanager` - runs a Flink JobManager in cluster mode and exposes a port for Flink and a port for the WebUI.
* `flink-taskmanager` - runs a Flink TaskManager and connects to the Flink Job Manager via static DNS name `jobmanager`.
* `flink-history-server` - runs a Flink History Server

Usage
=====

### Build

You only need to build the Docker image if you have changed Dockerfile or the startup shell script, otherwise skip to the next step and start using directly.

To build, get the code from Github, change as desired and build an image by running `docker build .`

### Run locally

Get the `docker-compose.yml` from Github and then use the following snippets

**Start Zeppelin, JobManager and TaskManager**

`docker-compose up -d` will start in background Zeppelin linked with one JobManager with a single TaskManager and the History Server.

**Scale TaskManagers**

`docker-compose scale taskmanager=5` will scale to 5 TaskManagers.

**Accessing Apache Zeppelin**

Navigate to [http://localhost:8080](http://localhost:8080)

Navigate to the interpreter page in order to update flink properties setting `host=jobamanager`

**Accessing Flink Web Dashboard**

Navigate to [http://localhost:8081](http://localhost:8081)

**Stop Zeppelin-Flink Cluster**

`docker-compose down` shuts down the cluster.

Disclaimer
==========

Apache®, Apache Flink™, Flink™, and the Apache feather logo are trademarks of [The Apache Software Foundation](http://apache.org).