# laraApp
Vivid and working instructions on how to deploy a laravel 5.4 and above app to a subdomain when using a shared host

## `First`
Create your subdomain with its root pointing to a folder under your public_html<br>
> E.g:  `http://app.example.com`<br>
> root: `/home/public_html/app/`

## `Second`
Create a folder within the new subdomain<br>
> E.g:  `http://app.example.com/realsite`<br>
> root: `/home/public_html/app/realsite`

## `Third`
Upload you laravel website (zip up everything within the laravel web app and upload) to the **realsite** folder directory.
This would make your folder structure have the likes of **app, routes, config** in it.

## `Fourth`
Copy these files from your **http://app.example.com/realsite/public/**
- .htaccess
- index.php
- robots.txt
- web.config
Paste them in **http://app.example.com/**

## `Fifth`
Next, navigate to the files you just pasted in **http://app.example.com/** and lets edit some lines in the **index.php** file.
- `require __DIR__.'/../vendor/autoload.php';`
- [x] `require __DIR__.'/realsite/vendor/autoload.php';`

- `$app = require_once __DIR__.'/../bootstrap/app.php';`
- [x] `$app = require_once __DIR__.'/realsite/bootstrap/app.php';`

## `Last`
The last thing to get your laravel app up and running on your subdomain will be the **.htaccess** trick. Still on your **http://app.example.com/** directory, open up your **.htaccess** file and copy these lines to replace it:

> <IfModule mod_rewrite.c>
>    <IfModule mod_negotiation.c>
>        Options -MultiViews
>    </IfModule>
>
>    RewriteEngine On
>
>    # Redirect Trailing Slashes If Not A Folder...
>    RewriteCond %{REQUEST_FILENAME} !-d
>    RewriteRule ^(.*)/$ /$1 [L,R=301]
>
>    # Handle Front Controller...
>    RewriteCond %{REQUEST_FILENAME} !-d
>    RewriteCond %{REQUEST_FILENAME} !-f
>    RewriteRule ^ index.php [L]
>   
>    <Files .env>
>    order allow,deny
>    Deny from all
>    </Files>
>
>    Options -Indexes
>
>    # Handle Authorization Header
>    RewriteCond %{HTTP:Authorization} .
>    RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
> </IfModule>
>
> # php -- BEGIN cPanel-generated handler, do not edit
> # Set the “ea-php72” package as the default “PHP” programming language.
> <IfModule mime_module>
>   AddType application/x-httpd-ea-php72 .php .php7 .phtml
> </IfModule>
> # php -- END cPanel-generated handler, do not edit


### AND THERE WE GO... **http://app.example.com/** SHOULD BE ACCESSIBLE VIA THE WEB URL...

## HOPE THIS HELPS SOMEONE!!!
