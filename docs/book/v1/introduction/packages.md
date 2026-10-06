# Packages

## Summary

The six direct Composer dependencies Dotkernel Light installs, and what each one does.

## Details

* `dotkernel/dot-errorhandler` - Logging Error Handler for Middleware Applications
* `laminas/laminas-component-installer` - Composer plugin for injecting modules and configuration providers into application configuration
* `laminas/laminas-config-aggregator` - Lightweight library for collecting and merging configuration from different sources
* `mezzio/mezzio` - PSR-15 Middleware Microframework
* `mezzio/mezzio-fastroute` - FastRoute integration for Mezzio
* `mezzio/mezzio-twigrenderer` - Twig integration for Mezzio

## FAQ

**Q: How many direct dependencies does Dotkernel Light have?**
A: Six, listed above — the same six declared under `require` in `composer.json`.

**Q: Which package handles routing?**
A: `mezzio/mezzio-fastroute`, FastRoute's integration for Mezzio.

**Q: Which package renders the Twig templates?**
A: `mezzio/mezzio-twigrenderer`.
