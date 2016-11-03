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
