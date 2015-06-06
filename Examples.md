# 'Replace' Example #

  1. Create a new text file and call it "replace-demo.xml"
  1. Add the minimum required xml structure

**Input**
```
$var = 'ABC';
```

**Script**
```
<?xml version="1.0" encoding="UTF-8"?>
<modification>
	<id>Replace ABC with 123</id>
	<version>1.0</version>
	<vqmver>2.X</vqmver>
	<author>xxx</author>
	<file name="path/to/myfile.php">
		<operation info="replace ABC with 123">
			<search position="replace"><![CDATA[
			$var = 'ABC';
			]]></search>
			<add><![CDATA[
			$var = '123';
			]]></add>
		</operation>
	</file>
</modification>
```

**Output**
```
$var = '123';
```



# 'Before' Example #

  1. Create a new text file and call it "before-demo.xml"
  1. Add the minimum required xml structure

**Input**
```
$var = 'ABC';
```

**Script**
```
<?xml version="1.0" encoding="UTF-8"?>
<modification>
	<id>Before ABC, add 123</id>
	<version>1.0</version>
	<vqmver>2.X</vqmver>
	<author>xxx</author>
	<file name="path/to/myfile.php">
		<operation info="Before ABC, add 123">
			<search position="before"><![CDATA[
			$var = 'ABC';
			]]></search>
			<add><![CDATA[
			$var = '123';
			]]></add>
		</operation>
	</file>
</modification>
```

**Output**
```
$var = '123';
$var = 'ABC';
```



# 'After' Example #

  1. Create a new text file and call it "after-demo.xml"
  1. Add the minimum required xml structure

**Input**
```
$var = 'ABC';
```

**Script**
```
<?xml version="1.0" encoding="UTF-8"?>
<modification>
	<id>After ABC, add 123</id>
	<version>1.0</version>
	<vqmver>2.X</vqmver>
	<author>xxx</author>
	<file name="path/to/myfile.php">
		<operation info="After ABC, add 123">
			<search position="after"><![CDATA[
			$var = 'ABC';
			]]></search>
			<add><![CDATA[
			$var = '123';
			]]></add>
		</operation>
	</file>
</modification>
```

**Output**
```
$var = 'ABC';
$var = '123';
```


# `<`ignoreif`>` tag Example (2.3.0+) #

  1. Create a new text file and call it "ignoreif-after-demo.xml"
  1. Add the minimum required xml structure

**Input**
```
$var = 'ABC';
$var2 = 'XYZ';
```

**Script**
```
<?xml version="1.0" encoding="UTF-8"?>
<modification>
	<id>After ABC, add 123 only if XYZ not in file</id>
	<version>1.0</version>
	<vqmver>2.X</vqmver>
	<author>xxx</author>
	<file name="path/to/myfile.php">
		<operation info="After ABC, add 123 if XYZ not in file">
			<ignoreif><![CDATA[
			XYZ
			]]></ignoreif>
			<search position="after"><![CDATA[
			$var = 'ABC';
			]]></search>
			<add><![CDATA[
			$var = '123';
			]]></add>
		</operation>
	</file>
</modification>
```

**Output**
```
$var = 'ABC';
$var2 = 'XYZ';
```


# Multiple files and a base path example (2.3.0+) #

Sometimes you require adding the same modification to a number of files at once. Rather than having to do this for individual files and duplicating code for each, you can specify multiple files at once delimited by commas. You can also specify a base path to be used if the files are in a common directory. For example, suppose you want to replace ABC with 123 in the following files
> /path/to/a.php
> /path/to/b.php
> /path/to/c.php

  1. Create a new text file and call it "multi-file-demo.xml"
  1. Add the minimum required xml structure

**Input (all files)**
```
$var = 'ABC';
```

**Script**
```
<?xml version="1.0" encoding="UTF-8"?>
<modification>
	<id>Replace ABC with 123</id>
	<version>1.0</version>
	<vqmver>2.X</vqmver>
	<author>xxx</author>
	<file path="path/to/" name="a.php,b.php,c.php">
		<operation info="Replace ABC with 123">
			<search position="replace"><![CDATA[
			ABC
			]]></search>
			<add><![CDATA[
			123
			]]></add>
		</operation>
	</file>
</modification>
```

**Output (all files)**
```
$var = '123';
```


# 'Multi-line Replace' Example #

vQmod is limited to a single-line search, but you can use the "offset" attribute to blindly blanket additional lines of code in the replace.

  1. Create a new text file and call it "multi-replace-demo.xml"
  1. Add the minimum required xml structure
  1. To replace multiple lines we use the "offset" attribute with replace. Count the number of total lines to replace and subtract one as the main line is already covered by the replace command. In this example, there are 8 lines of code, so offset would be 7. **When possible it's advised to avoid doing this**

**Input**
```
public function index() {
	$a = rand();
	$b = rand();
	if ($a == $b) {
		echo 'oh noes';
		return false;
	}
}
```

**Script**
```
<?xml version="1.0" encoding="UTF-8"?>
<modification>
	<id>Replace many lines with one</id>
	<version>1.0</version>
	<vqmver>2.X</vqmver>
	<author>xxx</author>
	<file name="path/to/myfile.php">
		<operation info="Replace index function">
			<search position="replace" offset="7"><![CDATA[
			public function index() {
			]]></search>
			<add><![CDATA[
			public function index($arr = array()) {
				foreach ($arr as $a) {
					echo $a;
    				}
			}
			]]></add>
		</operation>
	</file>
</modification>
```

**Output**
```
public function index($arr = array()) {
	foreach ($arr as $a) {
		echo $a;
    	}
}







```
_Note there are still 7 blank lines. The offset clears the extra 7 lines of code from the input, but the replaced code is added in place of the initial line. So there will be 7 extra spaces after the new code, but it will not affect the code functionality, only the look of the vqcache file which is of no importance._