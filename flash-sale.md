ToC

# what is flash-sale
Flash sale is a marketing event where an eCommerce store sells specific products at a substantially discounted price for a very short period. The event could drive huge revenue growth. E.g. Black Friday, Double 11. In the meanwhile, it can cause traffic spike on the website. 

# consideration
There are several aspects we need to consider when designing the system. In this scenario, there are at least 2 services including order, and flash sale. 

## business user
We need a CMS system to enable business user to input attributes of products, which are to be saled during flash sale days, on the system. The attributes includes production name, description, effective date, end date, price, quantity, image, etc.  

## ui design
Page of flash sale event locates in specific campaign pages and only eligible customers can access the pages. This design can reduce invalid traffic during the event day.

## static resources
Static resouces like product image, name, etc could be stored in CDN rather than requesting from server every time. It will save bandwidth. CMS needs to integrate with CDN, after business user saving the product information, static resources are uploaded to CDN automatically.

## scalable
Scaling is accomplished by increasing/decreasing the number of deployed application. 

## cache
Cache system, like Redis, is used to store product information like product id, price. One of the commonly used cache system is Redis, we need to ensure cache system high availiability. Redis supports cluster and master/slave mode.

One of the commonly used scenario for cache is distributed lock, but lock is not a good design due to flash sale is a high concurrency with low-latency. Lock costs time and it makes system much more lower.

If you have many customers, consider to cache order information.

## message queue
Message queue system is used to decouple services, asychronously communication among services. 

Products to be sold are stored in message queue. Once customer gets the opportunity to reserve a product, that is to say the user request reaches the flash sale service. Flash sale service will retrieve product pre-stored in message queue and send a record to message queue to notify order system to generate a record in database.

We can see that data won't be written into disk or database in flash sale service in order to reduce I/O which is time cost operation. 

How to make sure the user request is sent to mq successfully? Whether data is inconsistant if flash service is down?
1. Message queue like Kafka supports acknowledge mode, when flash sale service get feedback from message queue that message sent to order service has reached message queeu, it will notify another message queue, the product message has been sucessfully consumed. 
2. If flash service is down before sending the message to downstream message queue, application won't notify product message queue, thus the message will be consumed by other running application after timeout.
3. If flash service is down when message reaches the product message queue, an order will be created in order system, but client app will get 500 error as http response. App client should raise a new request to order service checking if order exists.

In some application libraries, application will fetch more data than requested from message queue and cached the data in local memory to reduce further requests between application and message queue.

### kafka

**Some core parameters:**
```
// heartbeat timeout between client and server
kafka.properties.session.timeout.ms = 25000
// frequency of sending heartbeat
kafka.properties.heartbeat.interval.ms = 3000
// records pulled per request
kafka.consumer.max-poll-records=20
// message processing timeout
kafka.properties.max.poll.interval.ms=60000
```

**rebalancing** <br />
Following cases will trigger kafka rebalaning

1. increase or decrease kafka consumer.
2. not receiving heartbeat in time. (heartbeat.interval.ms)
3. exceed processing time. (max.poll.interval.ms)


## limit rate

## performance
### kafka


### redis


### postgres


## security
### risk control
When customer pays for the product, it needs to check user status to see if user is 


## security
### prevent malicious requests
 
## performance
