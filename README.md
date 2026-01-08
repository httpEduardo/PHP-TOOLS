# Selfoss - RSS Feed Aggregator

![PHP Version](https://img.shields.io/badge/PHP-%3E%3D5.6-blue.svg)
![License](https://img.shields.io/badge/license-GPLv3-green.svg)
![Version](https://img.shields.io/badge/version-2.16--SNAPSHOT-orange.svg)

## Overview

Selfoss is a multipurpose RSS feed reader and aggregator. It allows you to live stream and collect content from various sources including RSS feeds, Twitter, and other social media platforms in a single, easy-to-use web interface. This is a customized installation package maintained by HttpEdu.

## Features

- **RSS Feed Management**: Subscribe to and manage multiple RSS and Atom feeds
- **Multi-Source Support**: Aggregate content from RSS feeds, social media, and other sources
- **Web-Based Interface**: Access your feeds from any device with a web browser
- **Tag-Based Organization**: Organize your feeds with tags and filters
- **Search Functionality**: Full-text search across all your aggregated content
- **Mobile-Friendly**: Responsive design works on phones, tablets, and desktops
- **Privacy-Focused**: Self-hosted solution keeps your reading habits private
- **OPML Import/Export**: Easy migration from other feed readers
- **Automatic Updates**: Cron-based automatic feed updates
- **Multiple Database Options**: Supports MySQL, PostgreSQL, and SQLite

## Requirements

- **PHP**: Version 5.6 or higher
- **Database**: One of the following:
  - SQLite (default, no additional setup required)
  - MySQL 5.5+
  - PostgreSQL
- **Web Server**: Apache with mod_rewrite enabled (or nginx with proper configuration)
- **PHP Extensions**:
  - PDO
  - GD (for image processing)
  - cURL
  - mbstring
  - zlib
- **File Permissions**: Write access to data directories

## Installation

### Step 1: Upload Files

Upload all files from this package to your web server directory.

**Important**: Ensure you upload the invisible `.htaccess` files as they are required for proper URL routing.

### Step 2: Set Permissions

Make the following directories writable by the web server:

```bash
chmod -R 777 data/cache
chmod -R 777 data/favicons
chmod -R 777 data/logs
chmod -R 777 data/thumbnails
chmod -R 777 data/sqlite
chmod -R 777 public/
```

### Step 3: Configure Database

1. Copy the default configuration file:
   ```bash
   cp defaults.ini config.ini
   ```

2. Edit `config.ini` with your database credentials:
   - **For SQLite** (default): No changes needed
   - **For MySQL**: Update the following settings:
     ```ini
     db_type=mysql
     db_host=localhost
     db_database=selfoss
     db_username=your_username
     db_password=your_password
     db_port=3306
     ```

3. The database will be created automatically on first access
   - Ensure your database user has sufficient privileges to create tables and triggers

### Step 4: Access Selfoss

Navigate to your Selfoss URL in a web browser:

```
http://yourselfossurl.com/
```

### Step 5: Set Up Automatic Updates

Create a cron job to automatically update your feeds. Add one of the following to your crontab:

**Option A: Using the web endpoint**
```bash
*/15 * * * * curl -s http://yourselfossurl.com/update > /dev/null
```

**Option B: Using wget**
```bash
*/15 * * * * wget -O - http://yourselfossurl.com/update > /dev/null 2>&1
```

**Option C: Using the CLI script (recommended)**
```bash
*/15 * * * * cd /path/to/selfoss && php cliupdate.php > /dev/null
```

This example updates feeds every 15 minutes. Adjust the schedule as needed.

## Configuration

### Creating Your Configuration File

1. **Copy the defaults**: 
   ```bash
   cp defaults.ini config.ini
   ```

2. **Edit `config.ini`**: Add only the settings you want to override

3. **Important**: Keep the `[globals]` line at the top of the file

### Common Configuration Options

```ini
[globals]
; Database configuration
db_type=sqlite
db_file=data/sqlite/selfoss.db

; Authentication
username=admin
password=your_hashed_password
salt=change_this_random_string

; Display settings
items_perpage=50
items_lifetime=30

; UI customization
html_title=My RSS Reader
language=en
```

For a complete list of configuration options, see `defaults.ini`.

### Setting Up Authentication

To protect your Selfoss installation:

1. Generate a password hash (use the web interface)
2. Set `username` and `password` in `config.ini`
3. Change the `salt` value to a random string

### Configuration Examples

For more configuration examples, visit: [selfoss.HttpEdu](http://selfoss.HttpEdu)

## Usage

### Adding Feeds

1. Click the "+" button in the top navigation
2. Enter the feed URL
3. Choose tags and other options
4. Click "Save"

### Reading Articles

- Click on any article to expand and read
- Mark articles as read/unread with the checkmark icon
- Star important articles for later reference
- Use keyboard shortcuts for faster navigation

### Organizing Content

- **Tags**: Organize feeds by topic or category
- **Filters**: Use the sidebar to filter by source, tag, or status
- **Search**: Use the search box to find specific content

### Keyboard Shortcuts

- `space` - Open next article
- `n` - Jump to next article
- `v` - Open article in new tab
- `s` - Star/unstar current article
- `m` - Mark current article as read/unread
- `r` - Reload feeds
- `t` - Throw (mark as read and hide)

## Troubleshooting

### Common Issues

**Problem**: "Permission denied" errors
- **Solution**: Ensure the `data/` and `public/` directories are writable by the web server:
  ```bash
  chmod -R 777 data/
  chmod -R 777 public/
  ```

**Problem**: Feeds not updating automatically
- **Solution**: 
  - Verify your cron job is running correctly
  - Check `data/logs/default.log` for errors
  - Test the update manually: `php cliupdate.php`

**Problem**: Database connection errors
- **Solution**: 
  - Verify credentials in `config.ini`
  - Ensure the database exists and is accessible
  - Check that required PHP extensions (PDO, pdo_mysql/pdo_sqlite) are installed

**Problem**: Articles not loading or displaying incorrectly
- **Solution**: 
  - Clear your browser cache
  - Delete cached files: `rm -rf data/cache/*`
  - Check for JavaScript errors in browser console

**Problem**: Images not displaying
- **Solution**: 
  - Verify the `data/thumbnails` directory is writable
  - Check that PHP GD extension is installed
  - Review image proxy settings in `config.ini`

**Problem**: Updates fail with "trigger creation" error
- **Solution**: Grant your database user CREATE TRIGGER privileges

### Getting Help

For further questions, issues, or support, please use our support forum or open an issue on GitHub.

## Updating Selfoss

### Update Process

1. **Backup Your Data**
   ```bash
   # Backup database
   mysqldump -u username -p selfoss > selfoss_backup.sql
   
   # Backup data folder
   tar -czf selfoss_data_backup.tar.gz data/
   
   # Backup config
   cp config.ini config.ini.backup
   ```

2. **Download New Version**
   - Download the latest release
   - Extract to a temporary location

3. **Delete Old Files**
   - Delete all files EXCEPT:
     - `data/` folder
     - `config.ini` file

4. **Upload New Files**
   - Upload all new files and folders
   - **Important**: Include the invisible `.htaccess` files
   - Do NOT overwrite the `data/` folder

5. **Update Data Structure**
   - If upgrading from older versions, rename `/data/icons` to `/data/favicons`

6. **Clear Cached Assets**
   ```bash
   rm -f public/all-v*.css
   rm -f public/all-v*.js
   ```

7. **Update Configuration**
   - Compare `config.ini` with new `defaults.ini`
   - Add any new configuration options that are relevant
   - Review the changelog for configuration changes

8. **Clear Browser Cache**
   - Clear your browser cache to load new assets

9. **Verify Update**
   - Access Selfoss in your browser
   - The database will update automatically
   - Check that feeds are loading correctly

### Post-Update Checklist

- [ ] All feeds are visible and updating
- [ ] User authentication still works
- [ ] Images and favicons are loading
- [ ] No errors in `data/logs/default.log`

## OPML Import

Selfoss supports importing feed subscriptions from OPML files (used by most RSS readers).

### Import Steps

1. Navigate to the OPML import page:
   ```
   http://yourselfossurl.com/opml
   ```

2. Select your OPML file and upload

3. Feeds will be automatically imported with their categories as tags

### Google Reader Migration

If you're migrating from Google Reader:
1. Use Google Takeout to download your feed subscriptions as an OPML file
2. Import the OPML file as described above

## Mobile Apps

A third-party Android application is available for Selfoss, providing native mobile access to your feeds.

Search for "Selfoss" in the Google Play Store or F-Droid.

## Development

### Setting Up Development Environment

Selfoss uses git submodules for external libraries.

1. **Clone the repository**:
   ```bash
   git clone https://github.com/httpEduardo/PHP-TOOLS.git
   cd PHP-TOOLS
   ```

2. **Initialize submodules**:
   ```bash
   git submodule init
   git submodule update
   ```

3. **Install development dependencies**:
   ```bash
   npm install
   ```

### Building Assets

Use Grunt to build and minify assets:

```bash
grunt
```

## Credits

**Copyright** © 2015 HttpEdu  
**License**: GPLv3  
**Version**: 2.16-SNAPSHOT

### Contributors

Special thanks to all contributors who have submitted pull requests on GitHub. Your improvements and contributions make Selfoss better for everyone!

### Third-Party Libraries

Selfoss is built with the following excellent open-source libraries:

- **[FatFree PHP Framework](https://github.com/bcosca/fatfree)** - Lightweight PHP framework
- **[SimplePie](http://simplepie.org/)** - RSS feed parser
- **[jQuery](http://jquery.com/)** - JavaScript library
- **[jQuery UI](http://jqueryui.com/)** - User interface library
- **[WideImage](http://wideimage.sourceforge.net/)** - Image manipulation library
- **[htmLawed](http://www.bioinformatics.org/phplabware/internal_utilities/htmLawed/)** - HTML sanitizer
- **[PHP Universal Feed Generator](https://github.com/ajaxray/FeedWriter)** - RSS feed generation
- **[twitteroauth](https://github.com/abraham/twitteroauth)** - Twitter API library
- **[floIcon](http://www.phpclasses.org/package/3906-PHP-Read-and-write-images-from-ICO-files.html)** - ICO file handler
- **[jQuery hotkeys](https://github.com/tzuryby/jquery.hotkeys)** - Keyboard shortcuts
- **[jsmin](https://github.com/rgrove/jsmin-php)** - JavaScript minifier
- **[cssmin](https://code.google.com/archive/p/cssmin)** - CSS minifier
- **[Spectrum Colorpicker](https://github.com/bgrins/spectrum)** - Color picker widget
- **[jQuery custom content scroller](http://manos.malihu.gr/jquery-custom-content-scroller/)** - Custom scrollbar
- **[FullTextRSS](http://help.fivefilters.org/customer/portal/articles/223153-site-patterns)** - Full-text extraction
- **[Icon Source](http://www.artcoreillustrations.com/)** - UI icons

## License

This project is licensed under the GNU General Public License v3.0 (GPLv3).

See the [LICENSE](LICENSE) file for details.
