# Lazy Service Location

Service providers are only instantiated when explicitly requested, and then kept for the duration of the PHP run.

A locate event is not triggered until a named service is first requested, so if a service is not used, it has no overhead cost.

If no providers for a service are installed, the locate trigger has little cost, and any subsequent calls go straight to a NullProvider that minimizes resource use.

