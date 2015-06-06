# HISTORY #

### v2.5.0 - 2014-AUG-29 - Jay@jaygilford.com ###
  * Added caching of checked files to increase performance
  * Added error details of invalid XML files
  * Added negative offset for REPLACE position to remove lines before matched line instead of only after
  * Added `<search>` and `<add>` check to ensure present in each `<operation>`
  * Added second parameter to `modCheck` to allow specifying the Operations file path for a different source file
  * Changed `$_replaces` to `$replaces` in VQMod object to adhere to naming convention for public property
  * Change to `file()` method to increase performance
  * Changed regex path matching  to increase performance
  * Changed minor pieces of code to increase performance
  * Changed file\_put\_contents to lock files while saving ( bug fix for https://code.google.com/p/vqmod/issues/detail?id=167 )
  * Changed .htaccess security method to hopefully fix some servers having 500 ISE messages from Options -Indexes
  * Changed vqmod.php (Formatting cleanup)
  * Changed readme.txt files

**2.5.0 OpenCart specific changes**
  * Added attempted fix for weird installer bug ( https://code.google.com/p/vqmod/issues/detail?id=145 )
  * Added `admin/controller/extension/*.php` files to core vqmod\_opencart.xml
  * Changed vqmod\_opencart.xml to allow OC 2.0 integration

### v2.4.1 - 2013-JUL-29 - Jay@jaygilford.com ###
  * Fixed incompatibility with PHP versions lower than 5.3 for "_quotePath" callback
  * Turned devmode back on_

### v2.4.0 - 2013-JUL-28 - Jay@jaygilford.com ###
  * Added "ibefore" and "iafter" methods for "search" tags "position" attribute
  * Added case insensitivity for bug with certain windows installations
  * Added "required" attribute check for "vqmver" tag for incompatibility
  * Added file path being modified to error log
  * Added operation index of vQmod file tag to errorlog
  * Changed error messages to make them more concise
  * Changed "VQMod" class from instantiated to static, making it easier to integrate
  * Changed log file name format to make them consecutive ("0\_Sun.log", "1\_Mon.log" etc)
  * Changed PHP 5.5+ deprecated "e" regex modifier code to "preg\_replace\_callback" using "VQMod::_quotePath"
  * Removed position="all" attribute option_

**2.4.0 OpenCart specific changes**
  * Added seamless upgrade code to installer
  * Added XML header to "vqmod\_opencart.xml"
  * Changed "vqmod\_opencart.xml" to be greatly simplified and cover all php files in "/system/library" and "/system/engine" more consistently
  * Changed "admin" folder name variable to make it easier to edit in Oinstaller
  * Changed installer code to use new "VQMod::modCheck()" and "VQMod::bootup()" code

### v2.3.2 - 2013-FEB-27 - Jay@jaygilford.com ###
  * Fixed bug for mods.cache issue

### v2.3.1 - 2013-FEB-26 - Jay@jaygilford.com ###
  * Fixed bug with path replaces
  * Fixed bug with realpath never returning false
  * Added error handling for empty/invalid mods.cache
  * Added error handling for unknown ignoreif tag bug

### v2.3.0 - 2013-JAN-28 - Jay@jaygilford.com ###
  * Fixed minor bug with mods.cache - now refreshes cache when deleted
  * Added `<ignoreif>` tag to operations
  * Added path rewrites to make moved folders easier to manage
  * Multiple files can now be named inside `name=""` attribute, separated by commas
  * `path=""` attribute added to `<file>` tag to allow base prefix for multiple names
  * We now recommend adding a `info=""` attribute for operations to make it clearer what the operation does. This at present is purely optional but we advise adding for the benefit of others reading the files

### v2.2.2 - 2013-JAN-07 - Jay@jaygilford.com ###
  * Fixed invalid file path logging issue

### v2.2.1 - 2012-NOV-12 - Jay@jaygilford.com ###
  * Fixed invalid file path issue
  * Fixed empty search content issue
  * Added file change detection in original files
  * Fixed 1.4.X compatibility in XML for OpenCart

### v2.2.0 - 2012-OCT-28 - Jay@jaygilford.com ###
  * Removed cache lock code and implemented file modification detection
  * Added folder checks for vqcache and logs folder
  * Added rotational daily logs to curb large log file sizes
  * Added file being modded to log messages to make easier to debug
  * Fixed cache bug from 2.1.7
  * Added modifications caching to increase performance
  * Added cache path caching to increase performance
  * OpenCart Installer now checks files are writeable and notifies of any issues before attempting write

### v2.1.7 - 2012-AUG-16 - Qphoria@gmail.com ###
  * Updated xml/vqmod\_opencart.xml file to support OpenCart v1.5.4.
  * Added new "$cacheTime" variable with default of 60 secs
  * Deprecated "$useCache"

### v2.1.6 - 2012-MAR-15 - Qphoria@gmail.com ###
  * Added "error" attribute to the `<file>` tag
  * Moved main vQmod class to the top of the file to make version number easier to find

### v2.1.5 - 2011-NOV-10 - Qphoria@gmail.com ###
  * Prevent excessive ajax callbacks from constant rewriting of vqcache files

### v2.1.4 - 2011-OCT-28 - Jay@jaygilford.com ###
  * Added flock to read and write methods, to hopefully eliminate possible locked file problems

### v2.1.3 - 2011-OCT-16 - Jay@jaygilford.com ###
  * Fixed useCache accidentally taken out when adding in wildcard support

### v2.1.2 - 2011-OCT-09 - Jay@jaygilford.com ###
  * Fixed position="bottom" always returning 0
  * Fixed VQModObject::`_`skip not functioning
  * Fixed vqprotect.txt trying to load when it doesn't exist
  * Removed: vqprotect.txt file

### v2.1.1 - 2011-OCT-04 - Jay@jaygilford.com ###
  * Fixed inefficent regex bug
  * Fixed controller bug for opencart xml

### v2.1 - 2011-SEP-28 - Jay@jaygilford.com ###
  * Added wildcard support for filenames
  * Added back support for vqprotect.txt file
  * Added vqprotect.txt file
  * Added full commenting to the vqmod class
  * Added template fetch fix in vqmod\_opencart.xml

### v2.0.1 - 2011-SEP-20 - Jay@jaygilford.com ###
  * Missing referenced source files now log to file instead of die
  * Small tweaks

### v2.0 - 2011-SEP-14 - Jay@jaygilford.com ###
  * Complete Code Rewrite by JayG to be more object based
  * New "log" attribute for `<operation error="abort|skip|log">` to skip and log.

### v1.2.3 - 2011-JUN-21 - Qphoria@gmail.com ###
  * Fixed index explode issue per JayGs fix

### v1.2.2 - 2011-JUN-17 - Qphoria@gmail.com ###
  * Fixed index and empty source bugs per JNs suggestions

### v1.2.1 - 2011-JUN-17 - Qphoria@gmail.com ###
  * Fixed bug with index not being converted to an array
  * Fixed issue with invalid routes returning true on sourcefile (thanks JN)

### v1.2.0 - 2011-JUN-16 - Qphoria@gmail.com ###
  * Completely revamped logging to only write errors to vqmod.log. No point in writing the rest.
  * Added work around for realpath() on source path returning false on some servers
  * Added optional trim attribute to search tag (defaults to true).
  * Removed is\_numeric call on index since index is a comma-delimited field

### v1.1.0 - 2011-JUN-01 - Qphoria@gmail.com ###
  * Fixed another bug with source path on some servers
  * Changed fwrite to file\_put\_contents for tempfiles
  * Added write delays to tempfiles

### v1.0.9 - 2011-MAY-18 - Qphoria@gmail.com ###
  * Fixed bug with source path on some servers
  * Updated readme to be clearer
  * Added .htaccess to protect xml and log files

### v1.0.8 - 2011-JAN-19 - Qphoria@gmail.com ###
  * Fixed bug with a separate vqmod.log file being created in the admin
  * Added logging for source files that are referenced but don't exist to help troubleshoot

### v1.0.7 - 2011-JAN-18 - Qphoria@gmail.com ###
  * Default directory structure changed to put everything inside the /vqmod/ folder
  * xml files are now moved to /vqmod/xml/`*`.xml
  * Redesigned the construct to be simpler
  * Construct no longer requires a path or log option
  * New init() function handles initialization
  * Improved log function to use file\_put\_contents instead of fopen
  * Set logging = true by default

### v1.0.6 - 2011-JAN-12 - Qphoria@gmail.com ###
  * Added RegEx Support
  * Added new "all" position to replace entire file
  * Added new protected file list option to prevent some files from being modded for security
  * Additional performance improvements
  * Added divider lines to logging to improve readability between files
  * Added version to log print

### v1.0.5 - 2011-JAN-03 - Qphoria@gmail.com ###
  * Fixed bug with search "offset" duplicating the existing line

### v1.0.4 - 2010-Dec-30 - Qphoria@gmail.com ###
  * Fixed bug with search "index" attribute
  * Added "offset" attribute to search tag for blind multiline actions
  * Added more code checks to ensure xml values are valid

### v1.0.3 - 2010-Dec-29 - Qphoria@gmail.com ###
  * Overhauled the temp file and debug process to store the modified versions in the vqcache folder
  * Added new "index" attribute for search
  * Added useCache option for reusing cached versions
  * Added logging option
  * Added top and bottom positions to search for adding at the very top or bottom of a file
  * Added XML fileload handler
  * Updated the xml field legend
  * Added ability to write to the actual source file instead of virtually modding
  * Removed old debug mode and replaced with logging
  * Improved code performance
  * Changed vqdbg to vqcache
  * Updated Readme to be more robust

### v1.0.2 - 2010-Dec-23 - Qphoria@gmail.com ###
  * Added support for operation "error" attribute (skip, abort)
  * Added vqmver tag to identify the minimum version of VQMod needed for a mod to work

### v1.0.1 - 2010-Dec-23 - Qphoria@gmail.com ###
  * Fix for relative path when calling from a subfolder like "admin"

### v1.0.0 - 2010-Dec-22 - Qphoria@gmail.com ###
  * Original Version