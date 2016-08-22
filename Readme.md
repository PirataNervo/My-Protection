## My Protection

This plugin enhances your forum security and prevents data loss.

You should **never** tell anyone that you have it installed as the plugin outputs a fake 404 page when a user tries to access the plugin file directly.
&nbsp;
Open up inc/plugins/myprotection.php
And find this:
```php
define('MP_EMAIL', 'myemail@mail.com'); // change this to your email
define('MP_ADMIN_UID', 1); // change this to your admin user id (usually super admin)
define('MP_ADMINS_UIDS', '1'); // uid's of all admins on your forum seperated by a comma, for example: '1,3,5'
define('MP_EMAIL_DELAY', 600); // delay in seconds between emails are sent - 600 seconds by default = 10 minutes
define('MP_BLOCK_BOARD', 1); // set to 1 if you want MyProtection to immediatly block the usage of the forums once something wrong is found (recommended value: 1)
```
Do what the comments (what is after // ) say.

MyProection checks the following on each page load:
 * If MP_ADMIN_UID exists
	* If it doesn't, MP_EMAIL is emailed automatically and a backup of the database is made to admin/myprotection/backups - make sure it is chmod'd to 777
 * If each administrator was defined in MP_ADMINS_UIDS
	* If it finds one that wasn't, MP_EMAIL is emailed automatically and a backup of the database is made to admin/myprotection/backups - make sure it is chmod'd to 777
 * If the number of user id's set in MP_ADMINS_UIDS matches the number of administrators
	* If the number doesn't match, MP_EMAIL is emailed automatically and a backup of the database is made to admin/myprotection/backups - make sure it is chmod'd to 777
 * If there are any admins
	* If there no admins were found, MP_EMAIL is emailed automatically and a backup of the database is made to admin/myprotection/backups - make sure it is chmod'd to 777
 * If the uid's set in MP_ADMINS_UIDS exist in your database
	* If at least one of them doesn't, MP_EMAIL is emailed automatically and a backup of the database is made to admin/myprotection/backups - make sure it is chmod'd to 777
	
If anything of the above failed and if MP_BLOCK_BOARD is set to 1, the board is automatically closed (not the usual way) blocking the usage to everyone, including admins, displaying this message:
> I'm sorry, but you can't use this board until the administrator fixes the problem.

This MP_EMAIL_DELAY is used to set a delay between emails / checks once something wrong was found. By default it is set to 10 minutes (600 seconds).
If something wrong is found, every 600 seconds (by default) it checks everything again to check if the administrator has fixed the problem(s) already.

**In case you want to fix the board and you don't know how**
- Set MP_BLOCK_BOARD to 0 and make the necessary changes to your board - close it immediately!
- If something is missing (like posts, private messages, threads, etc), you can try to fix it by importing one of the backups made to admin/myprotection/backups

## Instructions

Download the latest release and open Readme.html file with your browser.

## Support
For support please visit [MyBB-Plugins.com](http://forums.mybb-plugins.com/ "MyBB-Plugins.com")