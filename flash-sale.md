ToC

# what is flash-sale
Flash sale is a marketing event where an eCommerce store sells specific products at a substantially discounted price for a very short period. The event could drive huge revenue growth. E.g. Black Friday, Double 11. In the meanwhile, it can cause traffic spike on the website. 

# consideration
There are several aspects we need to consider when designing the system.

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

## message queue
Message queue system is used to decouple services, asychronously communication among services. In this scenario, there are at least 3 services including payment, order, and flash sale. 
- Once customer suceessfully reserved a product, a record will be generated in flash sale service.
- Flash sale service send a record to in mq to notify order system to generate a record in database.
- Customer view the order and pay for the order processing in payment service.

We can see that 

How to make sure the user 

## security
### risk control
When customer pays for the product, it needs to check user status to see if user is 

## end user


## security
### prevent malicious requests


