# Using a Service

```php
// get Xoops object
$xoops = Xoops::getInstance();

// get provider
$provider = $xoops->service('Avatar');

// call contract method
$response = $provider->getAvatarUrl($user);

// get value from response
$avatar = $response->getValue();

// all together
$avatar = $xoops->service('Avatar')->getAvatarUrl($user)->getValue();
```

