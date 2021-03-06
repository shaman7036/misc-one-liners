# Apache configuration snips and utilities

## htaccess online checker

Good for rewrite rules: [http://htaccess.mwl.be/](http://htaccess.mwl.be/)


## Where

Rewrite rules can be applied in .haccess files or in configuration file.

Example:

```
#  cat /etc/httpd/conf.d/global_rewrite.conf
<IfModule mod_rewrite.c>
  RewriteEngine on
  RewriteCond %{HTTPS} off
  RewriteRule ^/?(.*) https://%{HTTP_HOST}:/$1 [R,L]
</IfModule>
```


## Examples

Enable rewrite engine (duh):
```
RewriteEngine on
```

Rewrite to enforce HTTPS:
```
RewriteCond %{HTTPS} off
RewriteRule ^/?(.*) https://my.site.tld/$1 [R,L]
```

or:
```
RewriteCond %{HTTPS} off
RewriteRule ^/?(.*) https://%{HTTP_HOST}:/$1 [R,L]
```

Prepend 'www":
```
RewriteCond %{HTTP_HOST} !^www\. [NC]
RewriteCond %{HTTP_HOST} ^([a-z.]+)$ [NC]
RewriteRule ^ http://www.%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```


Rewrite all to maintenance page:
```
RewriteRule ^(.*)$ /maintenance.html [L,QSA]
```

