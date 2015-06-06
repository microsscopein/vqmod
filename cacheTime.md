cacheTime removed as of v2.1.8

<s>
<h1>What is cacheTime?</h1>

Older versions of vQmod had a feature called "useCache" that would force vQmod vqcache files to always be reused and only generate them if they didn't exist. This was done initially to improve performance, even though performance wasn't really much of an issue.<br>
<br>
The problem is that when you add a new script that alters a file that already has a vqcache file, the new mod wouldn't be picked up until you deleted the existing vqcache file manually. This becomes a nuisance when people can't figure out why mods aren't working on their site. This is a constant problem with Aceshop, as they force useCache by default.<br>
<br>
So useCache was removed in v2.1.7 and replaced by a configurable <i>finite</i> timeout. Now vqcache files are regenerated after the cacheTime has expired.<br>
<br>
This allows performance caching while still offering a way to do dynamic regeneration for new mods. Each file is checked as it is loaded so it allows only a few files at a time to be regenerated, as opposed to all or none. The best of both worlds.<br>
<br>
<h1>Usage</h1>

By default, vQmod is set for 60 secs. This should be more than enough for everyone and you should not ever have to adjust this.<br>
<br>
But if you want to adjust it, you can add the following to your index.php file, under the line<br>
<pre><code>$vqmod = new VQMod();<br>
</code></pre>

So it looks like this:<br>
<pre><code>$vqmod = new VQMod();<br>
$vqmod-&gt;cacheTime = 300; //seconds<br>
</code></pre>
</s>