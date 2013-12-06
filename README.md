
Description
===========
This is a simple performance test tool to find out response time of nova instance creation under load.
This tool generates intended number of connections concurrently and listens on RabbitMQ queue to determine the instance 
successful creation and calculates the total time taken.

Two types of load generation algorithms implemented
. Connection Rate
. Number of Connections

Load is run as per the selected test type.

Limitations/Enhancements in pipe line
=====================================
. Take RabbitMQ configuration details through RESTful API

. Develop UI around this

. Ability to store various tests and get test results as we like

. Implement simultaneous user algorithms for load testing

. Configurable listen port for the webservice. Currently hardcoded on port 8080


Configure Test 
==============

Example for Connection Rate


```
POST /config
{
  "configname" : " test",
   "type" : "CONNECTIONRATE"
   "connectionrate" : 100,
   "novaurl": "http://10.244.66.250:8774/v2",
   "rmquser" : "guest",
   "rmqpass": "ravi",
   "authinfo" : {
          "username" : "demo",
          "password" : "ravi",
          "authurl" : "http://10.244.66.250:5000/v2.0",
          "tenantname":"demo"
  }
}
```

Example for Fixed number of Connections

```
POST /config
{
  "configname" : " test",
   "type" : "CONNECTIONS"
   "connections" : 100,
   "novaurl": "http://10.244.66.250:8774/v2",
   "rmquser" : "guest",
   "rmqpass": "ravi",
   "authinfo" : {
          "username" : "demo",
          "password" : "ravi",
          "authurl" : "http://10.244.66.250:5000/v2.0",
          "tenantname":"demo"
  }
}
```

Configure Server details 
========================

```
POST /server

{
  "flavorRef":"42",
  "imageRef":"bccd1cec-97ef-429a-816e-9f3050c3fb87",
   "name": "test"
}
```

Start the test
==============

```
POST /server/test/start
```


Stop the test
==============

```
POST /server/test/stop
```

Get the test results
====================
```
GET /server/test/result
```
Response is 
```
[{"request_id" : "req-d2fa6f22-fa9d-4ff2-ac4a-bd33b6e7e933", "start_time" :"2013-11-25 15:27:26.495363 -0800 PST", "response_duration": "5.364947s"}]
```
