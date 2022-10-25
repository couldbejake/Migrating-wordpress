# Migrating-wordpress

1. Copy DB, Files


2. Update site URL in DB (Replace ```<URL>``` with your site's URL)
```
update wp_options set option_value='<URL>' where option_name = 'siteurl';
update wp_options set option_value='<URL>' where option_name = 'home';
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

4. Update post URLs (Replace ```<URL>``` with your site's URL, and ```<OLD URL>``` with your site's old URL)
```
UPDATE wp_posts SET post_content = REPLACE(post_content,"<OLD URL>","<URL>")
```
5. Add ```define('FS_METHOD','direct');``` to wp-config.php file

6. If using Elementor, Elementor > Tools > Regenerate CSS

# Copying remote files

External -> Local

`scp username@domain:/home/xxx/xxx/11.jpeg /Users/username/Desktop/`

Local -> External

`scp /Users/username/Desktop/11.jpeg username@domain:/home/xxx/xxx`

To add a key do the following

`-i jakenelson-cpanel.pem`

If you get the errror `no host key alg RSA`, a temporary fix is to add 

```
HostKeyAlgorithms +ssh-rsa
PubkeyAcceptedKeyTypes +ssh-rsa
```

to the bottom of `/etc/ssh/sshd_config`, for a long-term fix, use newer key types
