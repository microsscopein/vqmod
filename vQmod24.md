# What is new in vQmod 2.4.x #

vQmod has been changed to be used as a static class instead of an instantiated class. This was done mainly because the way vQmod works as a common tool, it will never need more than a single instance of its class, so loading it statically is just simpler.

Full list of changes found in [r128](https://code.google.com/p/vqmod/source/detail?r=128)

# Static vs Instantiated #

Supposedly static is bit faster as well according to this
[article](http://moisadoru.wordpress.com/2010/03/02/static-call-versus-singleton-call-in-php/). But mainly it was done because vQmod doesn't need to ever be instantiated so it just makes sense to load it statically.

# How do I upgrade? #

The syntax of the vQmod calls in the index.php files has changed. But the built-in upgrade script will automatically upgrade you if using the older syntax so all you have to do is run the usual install url after copying over the new 2.4.x files:
```
http://mysite.com/vqmod/install/
```

Alternatively, you can still follow the manual install procedures here:
[Install\_OpenCart](Install_OpenCart.md)


**There is no change to the xml scripting syntax**