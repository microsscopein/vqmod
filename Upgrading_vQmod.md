# Introduction #

This explains the process of upgrading vQmod to a newer version.


# How to Upgrade vQmod #

  1. Download the latest version (use the opencart specific version if using opencart)
  1. Unzip the contents of the download. This should give you a folder called `vqmod` with an `install` and `xml` folder inside amongst others
  1. Upload that folder to your site's current `vqmod` folder via FTP. Any overwriting should be accepted if prompted. Do NOT drop the new folder on top of the current vqmod folder as that will generally upload into the directory, instead of over it. All files in the 2 folders will merge, and the new files will overwrite the old files. But all your existing xml files will be safe.

That's it!

You do **NOT** need to run the vQmod installer again for upgrade **UNLESS YOU ARE UPGRADING FROM BEFORE 2.4.0 TO 2.4.0 OR ABOVE**
You only need to run the installer if you've upgraded your site code and overwrote the index.php and admin/index.php files

If you are struggling to upgrade using the simple installer upgrade in OpenCart, simply upload fresh index.php files to both the main directory, and the admin directory and then run the installer