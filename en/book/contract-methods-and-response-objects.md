### Contract Methods and Response Objects



The service manager handles all response objects and calls the contract providers. To isolate the responsibilities for the response object, it is passed to the contract methods. 

As a result, the call to the service manager and the call to the contract implementation are different:



**Service call: **

```php
$response = $xoops->service("Avatar")->getAvatarUrl($userinfo);

```

**Contract definition: **

```php
public function getAvatarUrl($response, $userinfo);

```


