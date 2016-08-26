## Blackdove Datastructure plan

### define
Software, server and data storage architecture for fast scaling apps that require user and log tracking

### the structure

 - events api
 - client library
 - kafka
 - zookeeper
 - gobblin
 - hadoop
 - mapreduce
 - hive
 - looker
 - pig

  To get event data reliable trough the datapipe to the data warehouse, a trusted pipe is required [read #datapipes] The datapipes will have a realtime processed data structure which will be passed onto the data task runners (Gobblin ..) 

  The task runners will handle all data upstreams and push data into the warehouse, this will happen in batches

  Once data is registred in the pipe it has a time date marking which will be used to regenerate the data structure.

  [ CLIENT ] -> [..clientlib] -> [ EVENT API ] ->  [ KAFKA ] -_> [ *GOBLIN ] -> [ HADOOP ]
   -------------------------------------------------------------------------------------
          on event        on trigger       on trigger      batch task     storage


### datapipes
Kafka will be used as datapipe, kafka is an important step for not losing any data in the process of mass storage. The datapipeline is able to handle up-to as many as needed events per second, with the current setup a aprox of 42.453 events /s is reachable witouth any infrastructure range (6gb ram /zk , 6gb ram kafka (single brocker, single cluster), 4 gb ram for dockerized node js api that sends and upstreams the events)


### storage
Altough Kafka is great for dealing with the load, Kafka is not build for storing data longer than a specific time span, big data sets will make reproduce jobs exceptionally big and should be avoided at all times.


Instead of keeping the data inside of Kafka, a Gobblin taks will handle all the kafka data every xminutes, the data will be pushed inside a hadoop cluster which are build for large data storage

### processing
Data processing can be done by different services, the hadoop cluster will be opened up with hive and pig, so you can connect virutally any service that supports sql taks production or map reduce tasks.




~,b-ig <signed: Matti van de Weem, mvdweem@gmail.com>~ 
