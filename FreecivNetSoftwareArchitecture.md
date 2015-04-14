# Roadmap for new Freeciv.net System Architecture #


## Current System Architecture ##
This page documents the Freeciv.net System Architecture. The architecture has evolved into a scalable system of different nodes which perform specialized tasks. The overall architectural pattern of Freeciv.net is based on a client-server architecture. The system is mostly platform independent, but is well suited to run in a cloud computing setting, such as the Amazon EC2 platform. Hopefully this documentation will be informative for people interested in how Freeciv.net works, and of interest for similar projects creating scalable web applications using cloud computing. Most of the previous challenges with the architecture have been overcome.

Freeciv.net is a rich web application, which consists of the following components:

  * Freeciv.net Webclient: a Javascript AJAX application running in the user's web browser. This is the client in the system.
  * Varnish HTTP accelerator and cache. This is the service which handles all incoming connections to the Freeciv.net server nodes. It performs caching of static content, and redirecting requests to the correct civserver nodes.
  * Freeciv-web Java J2EE web application, running in Resin 4.0.2 and Java 6. This server process serves HTML, Javascript, images, and handles the user's sessions. It also handles several PHP applications, such as Facebook connect integration, form and wiki.
  * nginx HTTP server and reverse proxy. The most important function for nginx is to gzip packets which are sent to client.
  * Freeciv-proxy, a proxy translating civserver packets to JSON. Implemented in Python.
  * Publite2, a service for launching and monitoring civserver processes.
  * civserver, which is the Freeciv C server code running in separate processes. This is based on the Freeciv 2.1.x branch.
  * MySQL database and Amazon S3 Simple Storage Service for storage. The MySQL database handles the user-database, forum and wiki, while savegames are stored using Amazon S3.

![http://www.pvv.ntnu.no/~andrearo/freeciv-system-architecture.png](http://www.pvv.ntnu.no/~andrearo/freeciv-system-architecture.png)