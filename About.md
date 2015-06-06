# What is vQmod? #

vQmod™ (aka virtualQmod) gives the ability to create modification override "scripts" for included files in a controller-based web application.


# How does it work? #

Instead of modifying actual files to add custom modifications, source files are parsed "on-the-fly" right before any of the follow functions are called:

  * include()
  * include\_once()
  * require()
  * require\_once()

The source is then cloned to a temp file and modifications read from an external script file are made to that temp file. The temp file is then substituted for the real file in the include path. Now the modification is in place while the original file has not actually been altered. Remove the script file and the original source is loaded.


# Other Details #

  * The vQmod class is currently written in PHP and the script files are xml based, but the concept could be ported to any language and parsers could be created for any format.

  * Currently, OpenCart is the only fully tested and working platform that vQmod works with, but this is a concept that can work for other projects and platforms that are controller-based.

# Limitations #

vQmod relies on a controller based system that has a series of files that are linked and extended. There are some files that cannot be used with vQmod.
  * index.php - since this is the main file of the site, it has to load vQmod first for it to work on other pages. So you can't put the cart in front of the horse.
  * Standalone files - Files that are just standalone and don't extend or have no hierarchy will not work with vQmod. vQmod works by intercepting the "include" functions. So if file isn't being included or required, then it cannot be vQmodded
  * css & js files - These files are rendered at the browser level, not at the server level, so vQmod has no effect on these. You can, however, create new files and use vQmod to alter the tpl files to point to these new css/js files. Or you can put 

&lt;style&gt;

 and 

&lt;script&gt;

 tags directly into the tpl file.