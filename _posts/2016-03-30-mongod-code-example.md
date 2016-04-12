---
layout: post
title: code example on mongodb 
---





One good thing about mongdb is its ability to build spatial index. Using various command to do some query is actually handy. 


```
 db.data.find({"geometry.coordinates": {$within:{$box:[[ -177, -89],[ 170, 89]]}}}).limit(3)
 db.data.find({"geometry.coordinates": {$near:[ -177, -89], $maxDistance: 100}}).limit(3)
db.runCommand({geoNear:"data",near: [ 40, 40], maxDistance:5000000})

db.data.aggregate([{{$unwind: $geometry.coordinates}, $group: {_id: null, lonsum:{$avg: "$geometry.coordinates.0"}}}])

db.data.aggregate([{{$unwind: $geometry.coordinates}, {$group: {_id: null, lonsum:{$avg: "$geometry.coordinates.0"} } } } ])


db.data.aggregate([{$unwind: "$geometry.coordinates"}, 
                               {$group: {_id: null, 
                                         average: {$avg: "$geometry.coordinates.0"}
                                        }
                               },
                               {$project: {_id: 0, average: 1}}
                            ])


db.data.aggregate([{$unwind: "$geometry.coordinates"}, 
                               {$group: {_id: "$_id", 
                                         lng: {$first: "$geometry.coordinates"},
                                         lat: {$last: "$geometry.coordinates"}

                                        }
                               },
                               {$group: {_id: "$_id", 
                                         average: {$avg: "$lng"}
                                        }
                               },
                               {$project: {_id: 1, average: 1}}
                            ])


db.data.aggregate([{$unwind: "$geometry.coordinates"}, 
                               {$group: {_id: "$_id", 
                                         lng: {$first: "$geometry.coordinates"},
                                         lat: {$last: "$geometry.coordinates"}

                                        }
                               },
                               {$group: {_id: null, 
                                         avelng: {$avg: "$lng"},
                                         maxlng: {$max: "$lng"},
                                         minlng: {$min: "$lng"},
                                         avelat: {$avg: "$lat"},
                                         maxlat: {$max: "$lat"},
                                         minlat: {$min: "$lat"},
                                        }
                               },
                               {$project: {_id: 1, avelng: 1, maxlng: 1, minlng: 1, avelat: 1, maxlat: 1, minlat: 1}}
                            ])



 db.data.find({"geometry.coordinates": {$within:{$box:[[ -177, -89],[ 170, 89]]}}}).limit(3000)



```

Using docker to build a mongodb cluster is fast. 


```
Docker command
### Write a docker file
cd ddd/ddd
mkdir ddd
$touch Dockerfile

$notepad Dockerfile

$ docker build -t mymongo .

$ docker run -p 27017:27017 mymongo mongod

$ docker inspect ed18359d7107 | grep IPAddress | cut -d "" -f 4
     
$ docker-machine ip default

setup two containers:

$ docker run -p 28001:27017 --name mongo_instance_001 -d my/repo

$ docker run -p 28002:27017 --name mongo_instance_002 -d my/repo

ps -ef | grep mongo*
ps -ef | grep mongod
kill -9 pid

rm -rf /var/lib/mongo/mongod.lock

mongod -f /etc/mongod.conf --repair



 sudo mount -t vboxsf testdocker /mnt/testdocker

cd /mnt/testdocker

$ docker build -t mymongo .

sudo docker run --name rs_server1 -p 21117:27017 -d mymongo:latest --noprealloc --smallfiles --replSet rs1
sudo docker run --name rs_server2 -p 22117:27017 -d mymongo:latest --noprealloc --smallfiles --replSet rs1
sudo docker run --name rs_server3 -p 23117:27017 -d mymongo:latest --noprealloc --smallfiles --replSet rs1






docker tag d583c3ac45fd myname/server:latest


sudo docker exec 49653e5d0d6e  ifconfig
172.17.0.2

sudo docker exec 2a2ed8568441  ifconfig
172.17.0.3

sudo docker exec 9c79f18c55f2     ifconfig
172.17.0.4

docker exec -it 49653e5d0d6e  bash


 myconf = {"_id":"rs1","members":[
    {"_id":0,"host":"10.112.18.168:27017"},
    {"_id":1,"host":"10.112.18.28:27017"},
    {"_id":2,"host":"10.112.18.116:27017"}
     ]
     }


 myconf = {"_id":"rs1","members":[
    {"_id":0,"host":"10.112.18.168:27017"},
    {"_id":1,"host":"10.112.18.116:27017"},
    {"_id":2,"host":"10.112.18.148:27017"}
     ]
     }


 myconf = {"_id":"rs1","members":[
    {"_id":0,"host":"10.112.18.168:27017"},
    {"_id":1,"host":"10.112.18.116:27017"}
     ]
     }
cfg = rs.conf()
cfg.members[0].priority = 1
cfg.members[1].priority = 0.5
cfg.members[2].priority = 0.5

rs.initiate(myconf)
rs.reconfig(myconf, {force:true})
rs.reconfig(myconf)
docker run --name linuxtube -d ubuntu:latest /bin/bash -c "while true; do echo 1; done"

docker exec -it e7bb6cfd1a3a  bin/bash

```










