# Server Requirements

For production, we highly recommend a *nix based system.

## Webserver

### Apache >= 2.2

* mod_rewrite
* .htaccess support `(AllowOverride All)`

> The repository includes a default `.htaccess` file in the `public` folder.

### Nginx

You need to convert the provided Apache related `.htaccess` file into Nginx configuration instructions.

## PHP: 8.3, 8.4 or 8.5

Both mod_php and FCGI (FPM) are supported.

> These are the versions declared by `composer.json` in Dotkernel Light 1.5.0.
> PHP 8.5 was added in release 1.4.0 and PHP 8.2 was dropped in release 1.5.0, so stay on 1.4.x if you are pinned to PHP 8.2.

## Required Settings and Modules & Extensions

* memory_limit >= 128M
* mbstring
* Composer (added to $PATH)

## Recommended extensions

* opcache
* dom - if working with markup files structure (html, xml etc.)
* simplexml - working with xml files
* gd, exif - if working with images
* zlib, zip, bz2 - if compressing files
* curl (required if APIs are used)
