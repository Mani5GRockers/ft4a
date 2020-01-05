# ft4a
#### Xbtt tracker front-end in PHP + MySQL + PDO

### Prerequisites
- Nginx
- PHP 7.+
- MySQL server
- Xbt Tracker installed and running (https://github.com/OlafvdSpek/xbt)

### Site settings
- General site settings are in /web/includes/config.php
- First member (with ID #1) is admin and can access to web/admin/ part of the site.
- Admin part : Torrents list (+ edit and delete), Categories list (edit, delete, add), Licenses list (edit, delete, add), Members list (edit, delete, add), Message to all members, logs
- you can add/edit News upper part and footer text in web/includes/config.php

### Nginx settings
You have to add a "rewrite" part to Nginx virtualhost file like this :

``rewrite ^/c-(.*)$ /catpost.php?id=$1 last;``

``rewrite ^/l-(.*)$ /licpost.php?id=$1 last;``

``rewrite ^/a-(.*)-(.*)$ /archives.php?month=$1&year=$2 last;``

``if (!-d $request_filename){``

``   set $rule_2 1$rule_2;``

``}``

``if (!-f $request_filename){``

``   set $rule_2 2$rule_2;``

``}``

``if ($rule_2 = "21"){``

``   rewrite ^/(.*)$ /viewpost.php?id=$1 last;``

``}``

### MySQL settings
MySQL settings are in /web/includes/sql.php

### Crontab
/private/crontab.php : delete all info older that 5 minutes in xbt_announce_log table. Usefull for peers.php stats
You have to set up a crontab like this : ``*/5 * * * * php /var/www/example.com/private/crontab.php``

### Mail settings
You have to change Google Re-Captcha keys in :
- web/contact.php
- web/signup.php
- web/recup_pass.php

