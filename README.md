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

> `<IfModule mod_rewrite.c><br>`
>    `<IfModule mod_negotiation.c>`<br>
>        Options -MultiViews<br>
>    `</IfModule>`<br>
>
>    RewriteEngine On<br>
>
>    `# Redirect Trailing Slashes If Not A Folder...`<BR>
>    RewriteCond %{REQUEST_FILENAME} !-d<BR>
>    RewriteRule ^(.*)/$ /$1 [L,R=301]<br>
>
>    `# Handle Front Controller...` <br>
>    RewriteCond %{REQUEST_FILENAME} !-d<br>
>    RewriteCond %{REQUEST_FILENAME} !-f<br>
>    RewriteRule ^ index.php [L]<br>
>   
>    `<Files .env>` <br>
>    order allow,deny<br>
>    Deny from all<br>
>    `</Files>` <br>
>
>    Options -Indexes<br>
>
>    `# Handle Authorization Header`<br>
>    RewriteCond %{HTTP:Authorization} .<br>
>    RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]<br>
> `</IfModule>`<br>
>
> `# php -- BEGIN cPanel-generated handler, do not edit`<br>
> `# Set the “ea-php72” package as the default “PHP” programming language.`<br>
> `<IfModule mime_module>`<br>
>    AddType application/x-httpd-ea-php72 .php .php7 .phtml<br>
> `</IfModule>`<br>
> `# php -- END cPanel-generated handler, do not edit`<br>

Reference to the .htaccess file in this repo for comparison and cross-checking..

### AND THERE WE GO... **http://app.example.com/** SHOULD BE ACCESSIBLE VIA THE WEB URL...

## HOPE THIS HELPS SOMEONE!!!
