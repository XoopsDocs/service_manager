# 2.0 Service Manager 

To achieve the full benefit of the separation, XOOPS 2.6.0 alpha 3 introduced a **Service Manager** component. 

* Services located by **service name**, not provider 
* **Service interface** established by Contract 
* Returns a standardized Response object that includes **result, status and messages**



###  Service Manager Connection 

* Request is based on a well known interface 
* Actual provider does not matter to caller 
* No need to check for a specific module 
* If the service is not available, that status is returned just like any other error condition.


### Code Simplification 

**Direct Module Connection **

```php
if ($xoops->isActiveModule('notifications')) {
 $notification_handler = Notifications::getInstance()->getHandlerNotification();
 $notification_handler->triggerEvent('global', 0, 'category_created', $tags);
}
```

**Service Manager Connection**

```php
$xoops->service('Notify')->triggerEvent('global', 0, 'category_created', $tags);
```




