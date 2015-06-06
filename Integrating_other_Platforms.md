# Understanding the concept #

If you take a look at the [[About](About.md)] page you'll see the basic fundamental approach that vQmod takes for overriding files. Basically anywhere there is an "include" style call, vQmod is inserted in between the call, and the return of that call is then the new adjusted file that gets passed into the include call.

So for example:
```
  include('path/to/myfile.php');
```
becomes:
```
  include(VQMod::modCheck('path/to/myfile.php'));
```

  1. The modCheck function opens the original file
  1. The file is altered with the search/replace information
  1. The file is saved with a new name in the vqcache folder, leaving the original file untouched
  1. The new file path is then returned from the function and substituted into the include() call.


# Integration #

Now that the concept has been explained, you need to determine if your platform is able to be integrated with vQmod. What makes OpenCart so easy to vQmod is that most include() calls are done in a few common places.

First off, let's talk about index.php as it is the first file loaded in any platform. This file CANNOT be vQmodded because it is first in the chain. Something has to load vQmod so you can't put the cart before the horse. So in OpenCart, this file gets adjusted manually. You can see these steps in the [Install\_OpenCart](Install_OpenCart.md) link in the wiki. Ignore the auto-installer as that is a separate piece unrelated to vQmod itself.

In OpenCart, index.php and startup.php both load the static libraries as one of the first steps into the page load. Then the engine files are loaded. All libraries area loaded immediately, even before use. This can be frowned upon because it essentially means that libraries are loaded that may not be used, but with OpenCart, they will likely be used anyway so it just makes it easier for vQmod.

An alternative to loading everything upfront would be to use an [Autoload](http://www.php.net/manual/en/language.oop5.autoload.php) method. This would also make things easily vQmoddable because you could add vQmod into the custom autoload function.

Either way, OpenCart keeps all its loading into a few common "controller" engine files and all other files are subclassed from this. This means all calls go through this common point and vQmod can be added at these few checkpoints. This also means that files that are included through these checkpoints that have their own includes can easily be modded through vQmod so you don't have to make manual changes to these other files. It all goes through the hierarchy of the top level include call. This hierarchy design is critical to vQmod's abilities.

Additionally, the page being loaded needs to be included in some way to a routing function so that it can be altered. If it doesn't pass through anything then it isn't vQmoddable because as stated above, something needs to load the vQmod engine first.

So pages that end in .php won't be vQmoddable:
  * http://mysite.com/index.php
  * http://mysite.com/somepage.php
  * http://mysite.com/callback.php
  * etc

But pages that use a routing call will be:
  * http://mysite.com/index.php?route=product/product
  * http://mysite.com/mainpage.php?cPath=module/payment
  * http://mysite.com/home.php?page=1
  * etc


# Where it gets messy #

Places where it is difficult to add vQmod is in platforms that have include calls all over the place throughout multiple files with no common base. This means you need to manually edit each location to add the "modCheck" call before each include. This is fine if your platform is built with vQmod in the core, but if you are modding an existing platform with all these calls, that is a lot of manual editing to make and maintain.

I've tried vQmodding PHPBB3 and GetSimpleCMS. But gave up after a while because their structures just weren't right for vQmod. GetSimple's front end was likely doable, but the admin area was all statically called pages that ended in .php with no routing. PHPBB had includes all over that were difficult to track and maintain.

So each platform is different and may or may not work with vQmod.