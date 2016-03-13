---
layout: post
title: Play with Mongodb
---



## Impression:
Mongo DB is very flexible, it supports flexible schema. The basic structure is database - collection - document. Within the the same collection, the documents can have different data schema. The reason that Mongodb supports flexible schema is because it does not have a central data catalog, which results in a large data size, as each field name is saved repeatedly in each document.


## Large storage size:
 If you have been running mongodb for a while and end up with a large disk space consumed by Mongodb, you can do several things:  （1） run db.repairDatabase(), (2) setting the padding factor  to 1, (3) disable journaling.  (4) If you are new to mongodb, and you are surprised by the storage size of your data, the above options won't please you. Instead, you can try mongodb data compression options. The most effect data compression options come with wiredtiger engine. (a) Set up a sharded cluster., (b) set wiredtiger as default in the configuration file for replica sets, (c) You can have a mixture of windows and linux. Your replica set must all have wiredtiger engine option. (d) Your replica set can have different mongo edition. (e) It is better to have a  linux set as primary by setting the priority. (f) If your cluster has three nodes, you will end up have three ip address. It is better to enable static ip on all these machines. * An advantage of using docker is that you can set up three containers for mongodb, and you can use interal ips. (g) Your computer may have ip conflicts if you set static ip. As your primary is a linux, you can steal the ip back using linux asping. (h) You need to bindIp: 0.0.0.0 for your replica sets to communicate with each other. (I) Mongochef is a good interface for mongodb.  It is way better than robomong, as it supports wiredtiger engine. (j) Sometimes, it is wired that you cannot start mongo.  you can try to start it with mongod -f /etc/mongod.conf --repair. 


Notes: For a csv file with 32mb size: When switch from MMAPv1 engine to Wiredtiger engine, datasize changed from 145mb to 132mb, storage size changed from 166mb to 51mb, dbsize changed from 0.453gb to 0.061gb. The benefit of shortening name is noticeable for Wiredtiger engine. Datasize changed from 132mb to 115mb, storage size changed from 51 to 46mb, dbsize changed from 0.061 to 0.056gb. 



