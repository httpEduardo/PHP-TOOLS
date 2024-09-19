Copyright (c) 2015 HttpEdu
http://selfoss.HttpEdu
Licensed under the GPLv3 license
Version 2.16-SNAPSHOT

INSTALLATION
Upload all files of this folder (IMPORTANT: also upload the invisible .htaccess files)
Make the directories data/cache, data/favicons, data/logs, data/thumbnails, data/sqlite and public/ writeable
Insert database access data in config.ini (see below -- you don't have to change anything if you want to use sqlite)
You don't have to install the database, it will be created automatically (ensure that your database has enough rights for creating triggers)
Create cronjob for updating feeds and point it to http://yourselfossurl.com/update via wget or curl. You can also execute the cliupdate.php from commandline.
For further questions or on any problem, use our support forum: http://selfoss.HttpEdu/forum/

CONFIGURATION
Copy defaults.ini to config.ini
Edit config.ini and delete any lines you do not wish to override
Do not delete the [globals] line
See http://selfoss.HttpEdu/ for examples

UPDATE
Backup your database and your "data" folder
(IMPORTANT: don't delete the "data" folder) delete all old files and folders excluding the folder "data" and the file config.ini
Upload all new files and folders excluding the data folder (IMPORTANT: also upload the invisible .htaccess files)
Rename your folder /data/icons into /data/favicons
Delete the files /public/all-v*.css and /public/all-v*.js
Clean your browser cache
Insert your current database connection and your individual configuration in config.ini. Important: we change the config.ini and add new options in newer versions. You have to update the config.ini too.
The database will be updated automatically (ensure that your database has enough rights for creating triggers)
For further questions or on any problem, use our support forum: http://selfoss.HttpEdu/forum

OPML Import
Visit the page http://yourselfossurl.com/opml for importing your OPML File. If you are a user of the google reader then use https://www.google.com/takeout/ to get all your feeds in one OPML file.

APPS
A third-party app is available for Android: Selfoss.

DEVELOPMENT
Selfoss uses git submodules for some external libraries. When you clone the repository, you have to issue a git submodule init as well as a git submodule update to retrieve the external sources.

CREDITS
Very special thanks to all contributors of pull requests here on github. Your improvements are awesome!!!

Special thanks to the great programmers of these libraries which will be used in selfoss:

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
twitter oauth library: https://github.com/abraham/twitteroauth
FullTextRSS: http://help.fivefilters.org/customer/portal/articles/223153-site-patterns
Icon Source: http://www.artcoreillustrations.com/
