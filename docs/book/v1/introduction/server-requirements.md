# Server Requirements

For production, we highly recommend a *nix based system.

## Webserver

### Apache >= 2.2

* mod_rewrite
* .htaccess support `(AllowOverride All)`

> The repository includes a default `.htaccess` file in the `public` folder.

### Nginx

You need to convert the provided Apache related `.htaccess` file into Nginx configuration instructions.

## PHP >= 8.2

Both mod_php and FCGI (FPM) are supported.

## Required Settings and Modules & Extensions

* memory_limit >= 128M
* upload_max_filesize and post_max_size >= 100M (depending on your data)
* mbstring
* Composer (added to $PATH)

## Recommended extensions

* opcache
* dom - if working with markup files structure (html, xml etc.)
* simplexml - working with xml files
* gd, exif - if working with images
* zlib, zip, bz2 - if compressing files
* curl (required if APIs are used)
