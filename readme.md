
**Where does BackUpWordPress store the backup files?**

Backups are stored on your server in `/wp-content/backups`, you can change the directory.

**Important:** By default BackUpWordPress backs up everything in your site root as well as your database, this includes any non WordPress folders that happen to be in your site root. This does means that your backup directory can get quite large.

**What if I want to back up my site to another destination?**

**BackUpWordPress Pro supports Dropbox, Google Drive, Amazon S3, Rackspace, Azure, DreamObjects and FTP/SFTP. Check it out here:** [https://bwp.hmn.md](http://bwp.hmn.md/?utm_source=wordpress-org&utm_medium=plugin-page&utm_campaign=freeplugin)  

**How do I restore my site from a backup?**

You need to download the latest backup file either by clicking download on the backups page or via `FTP`. `Unzip` the files and upload all the files to your server overwriting your site. You can then import the database using your hosts database management tool (likely `phpMyAdmin`).

See this post for more details http://hmn.md/backupwordpress-how-to-restore-from-backup-files/.

**Does BackUpWordPress back up the backups directory?**

No.

**I\'m not receiving my backups by email**

Most servers have a filesize limit on email attachments, it\'s generally about 10mb. If your backup file is over that limit it won\'t be sent attached to the email, instead you should receive an email with a link to download the backup, if you aren\'t even receiving that then you likely have a mail issue on your server that you\'ll need to contact your host about.

**How many backups are stored by default?**

BackUpWordPress stores the last 10 backups by default.

**How long should a backup take?**

Unless your site is very large (many gigabytes) it should only take a few minutes to perform a back up, if your back up has been running for longer than an hour it\'s safe to assume that something has gone wrong, try de-activating and re-activating the plugin, if it keeps happening, contact support.

**What do I do if I get the wp-cron error message**

The issue is that your `wp-cron.php` is not returning a `200` response when hit with a http request originating from your own server, it could be several things, most of the time it\'s an issue with the server / site and not with BackUpWordPress.

Some things you can test are.

* Are scheduled posts working? (They use wp-cron too).
* Are you hosted on Heart Internet? (wp-cron is known not to work with them).
* If you click manual backup does it work?
	__( '* Try adding `define( \'ALTERNATE_WP_CRON\', true ); to your `wp-config.php`, do automatic backups work?', 'hmbkp' );
* Is your site private (I.E. is it behind some kind of authentication, maintenance plugin, .htaccess) if so wp-cron won\'t work until you remove it, if you are and you temporarily remove the authentication, do backups start working?

If you have tried all these then feel free to contact support.

**How to get BackUpWordPress working in Heart Internet**

**The script to be entered into the Heart Internet cPanel is:** `/usr/bin/php5 /home/sites/yourdomain.com/public_html/wp-cron.php` (note the space between php5 and the location of the file). The file `wp-cron.php` `chmod` must be set to `711`.  