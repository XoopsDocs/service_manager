# Service Manager Components

```php
namespace Xoops\Core\Service;
```

| File | Class Type | Description |
| --- | --- | --- |
| AbstractContract.php | Abstract Class | Contract boilerplate |
| Manager.php | Class | Manages service providers |
| NullProvider.php | Class | Provider used when no provider is installed |
| Provider.php | Class | Basic Provider support |
| Response.php | Class | Response used by all service providers |

```php
namespace XoopsCoreServiceContract;
```

This namespace holds interfaces that define all named services. For example, a contract for an 'Avatar' service would be

```php
Xoops\Core\Service\Contract\AvatarInterface
```

