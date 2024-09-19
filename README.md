Selfoss - Aggregator
Copyright (c) 2015 HttpEdu
Licensed under the GPLv3 license
Version 2.16-SNAPSHOT

Installation
Upload Files:
Upload all files of this folder (IMPORTANT: also upload the invisible .htaccess files).

Set Permissions:
Make the directories data/cache, data/favicons, data/logs, data/thumbnails, data/sqlite, and public/ writeable.

Configure Database:
Insert database access data in config.ini. If using sqlite, you don’t have to change anything.
The database will be created automatically (ensure that your database has enough rights for creating triggers).

Create Cron Job:
Create a cron job for updating feeds and point it to:

arduino

http://yourselfossurl.com/update
You can use wget or curl, or execute the cliupdate.php from the command line.

Need Help?
For further questions or issues, use our support forum.

Configuration
Copy Config:
Copy defaults.ini to config.ini.

Edit Config:
Edit config.ini and delete any lines you do not wish to override.
IMPORTANT: Do not delete the [globals] line.

Need Examples?
See selfoss.HttpEdu for examples.

Update Instructions
Backup:
Backup your database and the data folder. Do not delete the data folder.

Delete Old Files:
Delete all old files and folders, excluding the folder data and the file config.ini.

Upload New Files:
Upload all new files and folders, excluding the data folder.
IMPORTANT: Also upload the invisible .htaccess files.

Rename Icons Folder:
Rename /data/icons to /data/favicons.

Delete CSS and JS:
Delete the files /public/all-v*.css and /public/all-v*.js.

Clear Browser Cache:
Clean your browser cache.

Update Config:
Insert your current database connection and individual configurations in config.ini.
IMPORTANT: We update the config.ini in newer versions, so make sure to update it as well.

Database Update:
The database will be updated automatically (ensure that your database has enough rights for creating triggers).

Need Help?
For further questions or issues, use our support forum.

OPML Import
Visit the page:

arduino

http://yourselfossurl.com/opml
for importing your OPML file. If you are a Google Reader user, use Google Takeout to get all your feeds in one OPML file.

Apps
A third-party app is available for Android: Selfoss.

Development
Selfoss uses git submodules for some external libraries.
When you clone the repository, run the following commands to retrieve the external sources:

csharp

git submodule init
git submodule update
Credits
Special thanks to all contributors of pull requests on GitHub. Your improvements are awesome!
Additionally, special thanks to the developers of the libraries used in Selfoss:

FatFree PHP Framework: https://github.com/bcosca/fatfree
SimplePie: http://simplepie.org/
jQuery: http://jquery.com/
jQuery UI: http://jqueryui.com/
WideImage: http://wideimage.sourceforge.net/
htmLawed: http://www.bioinformatics.org/phplabware/internal_utilities/htmLawed/
PHP Universal Feed Generator: https://github.com/ajaxray/FeedWriter
twitteroauth: https://github.com/abraham/twitteroauth
floIcon: http://www.phpclasses.org/package/3906-PHP-Read-and-write-images-from-ICO-files.html
jQuery hotkeys: https://github.com/tzuryby/jquery.hotkeys
jsmin: https://github.com/rgrove/jsmin-php
cssmin: https://code.google.com/archive/p/cssmin
Spectrum Colorpicker: https://github.com/bgrins/spectrum
jQuery custom content scroller: http://manos.malihu.gr/jquery-custom-content-scroller/
FullTextRSS: http://help.fivefilters.org/customer/portal/articles/223153-site-patterns
Icon Source: http://www.artcoreillustrations.com/
