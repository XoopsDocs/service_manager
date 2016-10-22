# 3.0 Service Manager Components 
```php
namespace Xoops\Core\Service; 
```
||||
|--|--|--|
|AbstractContract.php |Abstract Class |Contract boilerplate |
|Manager.php |Class |Manages service providers |
|NullProvider.php |Class Provider used when no provider is installed |
|Provider.php |Class |Basic Provider support |
|Response.php |Class |Response used by all service providers |

```php
namespace XoopsCoreServiceContract; 
```
This namespace holds interfaces that define all named services. For example, a contract for an 'Avatar' service would be 
```
Xoops\Core\Service\Contract\AvatarInterface
```


### Service Provider 

Any module can implement a service provider. To provide a service, the module must respond to a **core.service.locate.name** event. This is usually accomplished using a **PreloadItem**. 

The locate event will supply a Provider object, and the module listener is expected to invoke the register() method of that object with an instance of its own provider implementation.


### Registering a Service Provider 

Avatar preload example: 
```php
/** 
* listen for core.service.locate.avatar event 
* 
* @param Provider $provider - provider object for requested service 
* 
* @return void 
*/ 
public static function eventCoreServiceLocateAvatar(Provider $provider) 
{ 
if (is_a($provider, 'XoopsCoreServiceProvider')) { 
$path = dirname(dirname(__FILE__)) . '/class/AvatarsProvider.php'; 
require $path; 
$object = new AvatarsProvider(); 
$provider->register($object); 
} 
}
```

### Service Provider Implementation 

Avatar example: 
```php
use Xoop\sCore\Service\Abstract\Contract; 
use Xoops\Core\Service\Contract\Avatar\Interface; 
class AvatarsProvider extends AbstractContract implements AvatarInterface 
{ 
// implementation goes here 
}
```


### Service Contract Example 
```php
namespace Xoops\Core\Service\Contract; 
interface AvatarInterface { 
const MODE = \Xoops\Core\Service\Manager::MODE_EXCLUSIVE; 

/** 
* @param Response $response \Xoops\Core\Service\Response object 
* @param mixed $userinfo XoopsUser object 
* 
* @return void - response->value absolute URL to avatar image 
*/ 

public function getAvatarUrl($response, $userinfo); 
/** 
* @param Response $response Xoops\Core\Service\Response object 
* @param mixed $userinfo XoopsUser object 
* 
* @return void - response->value absolute URL to edit function 
*/ 
public function getAvatarEditUrl($response, $userinfo); 
}
```

### Using a Service 
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

### Response Object 

* Response objects are managed automatically, so you should never need to instantiate one. 

* Useful methods when consuming a service
    
    * isSuccess() - true if service call was a success – getValue() 
    * get the value set by the call, can be any PHP type (scalar, array, object, etc.) If no provider is available, getValue() will return NULL. 
    * getErrorMessage – get array of messages 


* A Response object is the first argument to all Contract methods, but never included in the service() call 
    * A program calls the service manager 
        * The service manager: 
            * creates a response object 
            * calls the contract method 
            * returns the response object to the caller

### Contract Methods and Response Objects 

The service manager handles all response objects and calls the contract providers. To isolate the responsibilities for the response object, it is passed to the contract methods. As a result, the call to the service manager and the call to the contract implementation are different: 

**Service call: **

```php
$response = $xoops->service("Avatar")->getAvatarUrl($userinfo); 
```
**Contract definition: **

```php
public function getAvatarUrl($response, $userinfo);
```

### Lazy Service Location

Service providers are only instantiated when explicitly requested, and then kept for the duration of the PHP run.

A locate event is not triggered until a named service is first requested, so if a service is not used, it has no overhead cost.

If no providers for a service are installed, the locate trigger has little cost, and any subsequent calls go straight to a NullProvider that minimizes resource use.

### Service Manager Administration

* For simple cases, just install the provider module / extension and it will just work.

* For more complex cases use the services section in the administration area




