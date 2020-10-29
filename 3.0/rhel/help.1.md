% ORIENTDB(1)
% Roberto Franchini - r.franchini@orientdb.com
% November 15, 2016

# NAME
orientdb \- orientdb container image
  
# DESCRIPTION

The OrientDB image provides a containerized packaging of the OrientDB multi-model database. 
OrientDB is a 2nd Generation Distributed Graph Database with the flexibility of Documents in one product. 
It is a unique, true multi-model DBMS equipped to tackle today’s big data challenges and offers multi-master replication, 
sharding as well as more flexibility for modern, complex use cases. 

You can find more information on the OrientDB project from the project Web site (http://www.orientdb.com).

# USAGE
Describe how to run the image as a container and what factors might influence the behaviour of the image
itself. For example:

To set up the host system for use by the OrientDB container, run:

  atomic install rhel7/orientdb

To run the OrientDB container (after it is installed), run:

  atomic run rhel7/orientdb

To remove the OrientDB container (not the image) from your system, run:

  atomic uninstall rhel7/orientdb

To upgrade the OrientDB container from your system, run:

  atomic upgrade rhel7/orientdb