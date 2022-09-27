# Migrating-wordpress

1. Copy DB, Files


2. Update site URL in DB
```
update wp_options set option_value='http://3.8.93.74' where option_name = 'siteurl';
update wp_options set option_value='http://3.8.93.74' where option_name = 'home';
```

3. Update .htaccess

```
<IfModule mod_rewrite.c>

RewriteEngine On

RewriteBase /

RewriteRule ^index\.php$ - [L]

RewriteCond %{REQUEST_FILENAME} !-f

RewriteCond %{REQUEST_FILENAME} !-d

RewriteRule . /index.php [L]

</IfModule>
```

4. Update post URLs 
```
wp_posts SET post_content = REPLACE(post_content,"http://localhost","http://3.8.93.74")
```
5. Add ```define('FS_METHOD','direct');``` to wp-config.php file
