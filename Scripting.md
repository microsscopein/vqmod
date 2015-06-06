# The Golden Rules #
First things to set in your mind...
  1. The **`<search>`** tag can only be a single line, though doesn't have to be a whole line, as partial matches work too. You should learn how to use the _offset_ attribute to properly encompass all needed lines, but that doesn't mean you should encompass many lines. Instead of trying to include many lines from top down, try starting at the bottom and finding lines going up.
  1. Less is more! Whenever possible, try to match the smallest, yet still unique part of the code. That will improve the chances of being more future-resistant and avoid breaking other mods that may have changes close to yours.
  1. Pay attention to all the attribute options for each tag. There is a lot of power that is overlooked by people skimming over the syntax


# How to make vQmod Scripts #

There are two tools we recommend to help create vQmods if you don't want to edit them manually
  * UKSB's [vQGenerator](http://www.opencart-extensions.co.uk/vqgen/)
  * AvanOsch's [vQmoderator](http://www.opencart.com/index.php?route=extension/extension/info&extension_id=8247)
Both are completely free and open source


vQmod currently uses an xml formatted parser by default but other parsers can be created in the future as well.

A simple replace script example looks like this:
```
<?xml version="1.0" encoding="UTF-8"?>
<modification>
	<id>Replace 123 with ABC</id>
	<version>1.0.0</version>
	<vqmver>1.0.9</vqmver>
	<author>qphoria</author>
	
	<file name="relative/path/myfile.php">
		<operation>
		
			<search position="replace"><![CDATA[
			$var = '123';
			]]></search>
			
			<add><![CDATA[
			$var = 'ABC';
			]]></add>
			
		</operation>
	</file>	
</modification>
```
This script simply changes the value of a variable of "myfile.php" from "123" to "ABC" before it gets included.



# Syntax #

vQmod supports a number of parameters:

**modification**
  * This is the highest level of the file and there can only be one

**modification / id**
  * This is the name and description of the mod.
  * Format: Free form text. (Informational)

**modification / version**
  * This is the version of the mod.
  * Format: Number and Decimal (1.0.0) (Informational)

**modification / vqmver**
  * This is the minimum required version of VirtualQMod needed for the script to work.
  * Format: Number and Decimal (1.0.0) (Informational)
  * A required="true" attribute can be optionally set to disable the script if it doesn't meet the required version (Added from 2.4.0)

**modification / author**
  * This is the author of the mod.
  * Format: Free form text (Informational)

**modification / file**
  * This is the name of the file to modify
  * Requires attribute "name" as relative filename to the location of the main index.php file (e.g. catalog/controller/product/product.php). Can be delimited with commas to apply to multiple files at once (2.3.0 +) Name attribute supports a wildcard (`*`) character for dynamic path building. Each wildcard is limited to a single directory level.
```
     - catalog/view/theme/*/template/product/product.tpl
     - catalog/view/theme/*/*/product/product.tpl
     - etc
```
  * There can be multiple file tags in a single xml file. Each file can have its own set of operations
  * Optional attribute "path" can be used to prefix file name's to avoid repetition. This is simply prepended to the file names and _no_ validation is attempted (2.3.0 +)
  * Optional attribute "error" set to log|skip|abort
    * _skip_ means it will simply ignore this file.
    * _log_ is the same as skip, but logs the error. **(default)**
    * _abort_ means to log the error and cancel the remaining operations in that particular xml script. It does not revert changes to other files already made in that script and doesn't stop other xml files.
    * **Wildcard paths will ignore the "error" attribute completely**

**modification / file / operation**
  * This is the wrapper of the actual operation occurring.
  * There can be multiple operations to the same _file_ tag.
  * Optional attribute "info" suggested. May be used by vQmod/vQmod Manager for OC in the future but at present isn't used. This is however ideal for making files easier to read
  * Optional attribute "error" set to skip|log|abort
    * _skip_ means all other operations will be applied even if one cannot. There will be no error in the log.
    * _log_ is the same as skip, but logs the error.
    * _abort_ means to log the error and revert to the original source. **(default)**

**modification / file / operation / ignoreif**
  * This allows for a search to be made on a file. This search works across _multiple lines_ not just single lines. This tag is optional and if the search is found, the operation is skipped
    * Optional attribute "regex' set to true|false. Format of data inside tag then requires delimiters for regex as it uses the standard preg\_match method for php. This attribute defaults to false

**modification / file / operation / search**
  * This is the first required step of the operation.
  * <font color='#ff0000'><b>Can only search single lines</b></font>, both fully and partially. But _offset_ and _index_ attributes will assist.
  * Automatically trims whitespace and linebreaks
  * One per _operation_ tag
  * Recommended to use CDATA tags to wrap code.
  * Required attribute "position" set to before|after|replace|top|bottom|~~all~~|ibefore|iafter.
    * _replace_ will replace the data in the _search_ tag with the data in the _add_ tag. (default)
    * _before_ will insert the _add_ data before the _search_ data
    * _after_ will insert the _add_ data after the _search_ data
    * _top_ will insert the _add_ data at the top of the file. The _search_ data is ignored.
    * _bottom_ will insert the _add_ data at the bottom of the file. The _search_ data is ignored.
    * ~~_all_ will completely replace all the code in the file with the _add_ data. The _search_ data is ignored.~~ Deprecated as of 2.4.0
    * _ibefore_ will insert the code before the search inline instead of the line before
    * _iafter_ will insert the code afterthe search inline instead of the line before
  * Optional attribute "offset" to work with the position
    * if the search position is before and offset 3 it will put the _add_ data before the line, 3 lines above the searched line
    * if the search position is after and offset 3 it will put the _add_ data after the line, 3 lines below the searched line
    * if the search position is replace and offset 3 it will remove the code from the search line and the next 3 lines and replace it with the _add_ data
    * if the search position is top and offset 3 it will put the code before the line, 3 lines below the top of the file
    * if the search position is bottom and offset 3 it will put the code after the line, 3 lines above the bottom of the file
  * Optional attribute "index" for specifying which instances of a search tag should be acted on
    * If the search string is "echo" and there are 5 echos in the file, but only want to replace the 1st and 3rd, use index="1,3"
    * Comma delimited for multiple instances starting with "1"
    * Leave out or set to FALSE to replace all instances. (default)
  * Optional attribute "regex" for specifying whether or not to search a regex pattern.
    * If true, the _search_ data should be a valid regex pattern
    * Leave out or set to FALSE to use normal string search (default)
    * Does not apply to `ibefore` and `iafter`
  * Optional attribute "trim" set to true|false
    * true will trim away whitespace and linebreaks.
    * leave out or set to true to trim. (default is true)

**modification / file / operation / add**
  * This is the second required step of the operation.
  * Can be multiple lines
  * One per operation.
  * Location of added data depends on the position attribute of the _search_ command.
  * Use CDATA tags to wrap code.
  * Optional attribute "trim" set to true|false
    * true will trim away whitespace and linebreaks.
    * leave out or set to false to not trim. (default is false)

**`<![CDATA[  ]]>`**
  * These are called CDATA tags and they are used by xml to specify that the data between should not be evaluated. It's recommended you always use these for data between the search and add operation tags