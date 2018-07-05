# Response Object

* Response objects are managed automatically, so you should never need to instantiate one.
* Useful methods when consuming a service
  * isSuccess\(\) - true if service call was a success – getValue\(\)
  * get the value set by the call, can be any PHP type \(scalar, array, object, etc.\) If no provider is available, getValue\(\) will return NULL.
  * getErrorMessage – get array of messages
* A Response object is the first argument to all Contract methods, but never included in the service\(\) call
  * A program calls the service manager
  * The service manager:
  * creates a response object
  * calls the contract method
  * returns the response object to the caller

