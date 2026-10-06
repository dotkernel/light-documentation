# Development mode

## Summary

How to enable, disable and check development mode — and when you actually need to run these commands yourself.

## Details

> `composer create-project dotkernel/light dk` already runs `composer development-enable` for you.
> You only need the command below after running `composer development-disable`, or if you installed by cloning the repository directly.

If you're installing the project for development, make sure you have development mode enabled, by running:

```shell
composer development-enable
```

You can disable development mode by running:

```shell
composer development-disable
```

You can check if you have development mode enabled by running:

```shell
composer development-status
```

## FAQ

**Q: Do I need to run `composer development-enable` after `composer create-project`?**
A: No — `composer create-project` already runs it for you.

**Q: How do I check which mode I'm in?**
A: Run `composer development-status`.

**Q: What does development mode change?**
A: It turns the debug flag on and configuration caching off, and clears any existing config cache.
