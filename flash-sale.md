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

## product cache



## security
### risk control
When customer pays for the product, it needs to check user status to see if user is 

## end user


## security
### prevent malicious requests


