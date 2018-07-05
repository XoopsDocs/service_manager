# Service Provider

Any module can implement a service provider. To provide a service, the module must respond to a **core.service.locate.name** event. This is usually accomplished using a **PreloadItem**.

The locate event will supply a Provider object, and the module listener is expected to invoke the register\(\) method of that object with an instance of its own provider implementation.

