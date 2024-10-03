# Server Requirements

For production, we highly recommend a *nix based system.

## Webserver

### Apache >= 2.2

* mod_rewrite
* .htaccess support `(AllowOverride All)`

> The repo contains in the public folder a default `.htacess` file

### NGINX

* you need to convert the provided Apache related `.htaccess` file into Nginx configuration instructions

## PHP >= 8.2

Both mod_php and FCGI (FPM) are supported.

## Required Settings and Modules & Extensions

* memory_limit >= 128M
* upload_max_filesize and post_max_size >= 100M (depending on your data)
* mbstring
* CLI SAPI (for Cron Jobs)
* Composer (added to $PATH)

## RDBMS

* MariaDB >= 10.11 LTS

## Recommended extensions

* opcache
* pdo_mysql or mysqli (if using MySQL or MariaDB as RDBMS)
* dom - if working with markup files structure (html, xml etc.)
* simplexml - working with xml files
* gd, exif - if working with images
* zlib, zip, bz2 - if compressing files
* curl (required if APIs are used)
* sqlite3 - for tests
