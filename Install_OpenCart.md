#How to install vQmod on OpenCart


# New Install Video Tutorial (OpenCart) #
<a href='http://www.youtube.com/watch?feature=player_embedded&v=ezS1jWoMmjc' target='_blank'><img src='http://img.youtube.com/vi/ezS1jWoMmjc/0.jpg' width='425' height=344 /></a>

# Installing on OpenCart #

vQmod works on both OpenCart 1.4.x and 1.5.x



# How to install using Autoinstaller #

  1. Download the latest version that has "opencart" in the title from
    * http://code.google.com/p/vqmod
  1. Using FTP, upload the "vqmod" folder from the zip to the root of your opencart store.
  1. Be sure the vqmod folder and the vqmod/vqcache folders are writable (either 755 or 777).
    * Also be sure index.php and admin/index.php are writable.
      * If not sure which you need, first try 755.
      * If you get errors about permissions, then try 777.
  1. Goto http://www.yoursite.com/vqmod/install
  1. You should get a success message. If not, check permissions above and try again
  1. Load your store homepage and verify it works.
  1. Using FTP, verify that there are new "vq" files in the "vqmod/vqcache" folder.
  1. If yes, then you are ready to start downloading or creating vQmod scripts, otherwise ask for assistance.
Done!


  * **DO NOT DELETE THE INSTALL FOLDER!**
  * **YOU MUST RUN THE INSTALLER EVERY TIME YOU UPGRADE OPENCART!!**
  * **THERE IS NO DANGER OF RE-RUNNING THE INSTALLER!**


# How to install Manually (2.4.0+) #

  1. Download the latest version that has "opencart" in the title from
    * http://code.google.com/p/vqmod
  1. Using FTP, upload the "vqmod" folder from the zip to the root of your opencart store.
  1. Be sure the vqmod folder and the vqmod/vqcache folders are writable (either 755 or 777).
    * Also be sure index.php and admin/index.php are writable.
      * If not sure which you need, first try 755.
      * If you get errors about permissions, then try 777.
  1. Edit your **index.php** file
  1. FIND:
```
// Startup
require_once(DIR_SYSTEM . 'startup.php');

// Application Classes
require_once(DIR_SYSTEM . 'library/customer.php');
require_once(DIR_SYSTEM . 'library/currency.php');
require_once(DIR_SYSTEM . 'library/tax.php');
require_once(DIR_SYSTEM . 'library/weight.php');
require_once(DIR_SYSTEM . 'library/length.php');
require_once(DIR_SYSTEM . 'library/cart.php');
require_once(DIR_SYSTEM . 'library/affiliate.php');
```
  1. REPLACE WITH:
```
// vQmod
require_once('./vqmod/vqmod.php');
VQMod::bootup();

// VQMODDED Startup
require_once(VQMod::modCheck(DIR_SYSTEM . 'startup.php'));

// Application Classes
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/customer.php'));
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/currency.php'));
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/tax.php'));
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/weight.php'));
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/length.php'));
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/cart.php'));
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/affiliate.php'));
```
**Note the affiliate library file may not exist on older systems**. Basically any `require_once(DIR_SYSTEM . 'library/xxxxxxxx.php');`
needs to be changed to use the `vqmod->modCheck` above in the same format. This also applies to any additional require\_once files in the next step
  1. Edit your **admin/index.php** file
  1. FIND:
```
// Startup
require_once(DIR_SYSTEM . 'startup.php');

// Application Classes
require_once(DIR_SYSTEM . 'library/currency.php');
require_once(DIR_SYSTEM . 'library/user.php'));
require_once(DIR_SYSTEM . 'library/weight.php');
require_once(DIR_SYSTEM . 'library/length.php');
```
  1. REPLACE WITH:
```
// vQmod
require_once('../vqmod/vqmod.php');
VQMod::bootup();

// VQMODDED Startup
require_once(VQMod::modCheck(DIR_SYSTEM . 'startup.php'));

// Application Classes
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/currency.php'));
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/user.php'));
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/weight.php'));
require_once(VQMod::modCheck(DIR_SYSTEM . 'library/length.php'));
```
  1. Load your store homepage and verify it works.
  1. Using FTP, verify that there are new "vq" files in the "vqmod/vqcache" folder.
  1. If yes, then you are ready to start downloading or creating vQmod scripts.
Done!

# How to install manually (pre 2.4.0) #
https://code.google.com/p/vqmod/source/browse/wiki/Install_OpenCart.wiki?r=104