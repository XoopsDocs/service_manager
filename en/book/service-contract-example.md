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
