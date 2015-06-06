useCache removed as of v2.1.7

<s>

<h1>About useCache</h1>

vQmod was designed to load, patch, and substitute files on the fly. This happens extremely quickly but when dealing with high-traffic sites, it is possible that multiple pages loading at the same time will both try to patch the files at the same time. This can cause occasional errors.<br>
<br>
This also happens in the case where there are a lot of ajax callbacks at the same time. Ajax callbacks fire at a much faster rate as they only load bits of the page. But the full rewrite of the files still triggers.<br>
<br>
<del>We are looking at better ways to get around this, but the quick solution is to enable useCache.</del>

As of v2.1.5 we've added a pseudo-cache feature that basically caches a file for 3 seconds. This means that within the same 3 secs, if another page load tries to reload that same file, it will use the cached version. This will likely be made configurable in the future so that you could use something like:<br>
<code>$vqmod-&gt;useCache = 3600;</code>
which would force it to use the same version for one hour.<br>
For now, it is either on of off.<br>
<br>
To enable useCache on your site...<br>
<br>
<ol><li>EDIT your index.php and admin/index.php files<br>
</li><li>FIND:<br>
<pre><code>    $vqmod = new VQMod();<br>
</code></pre>
</li><li>AFTER, ADD:<br>
<pre><code>    $vqmod-&gt;useCache = true;<br>
</code></pre></li></ol>

useCache will force vQmod to reuse the previously generated version of the new substitution file after it has been created the first time. Instead of generating it over and over again each time the page is loaded.<br>
<br>
<br>
<h1>Important Notes!</h1>

When using useCache, you must keep the following in mind<br>
<ul><li>Since the substitution files are now only loaded if they don't already exist, when you add or change an xml script, you need to blow away all the files inside the vqcache folder so that the new changes can be generated the first time. Otherwise, you may not see the changes that a script has made because it is using the cached version of the changes.<br>
</li><li>If you upgrade your index files on your site, you will need to re-add this change.</s>