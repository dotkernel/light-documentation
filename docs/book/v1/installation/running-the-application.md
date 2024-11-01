# Running the application

We recommend running your applications in WSL:

- make sure you have [WSL](https://github.com/dotkernel/development/blob/main/wsl/README.md) installed on your system
- currently we provide a distro implementations for [AlmaLinux9](https://github.com/dotkernel/development/blob/main/wsl/os/almalinux9/README.md)
- install the application in a virtualhost as recommended by the chosen distro
- set `$baseUrl` in **config/autoload/local.php** to the address of the virtualhost
- run the application by opening the virtualhost address in your browser

You should see the `Dotkernel Light` welcome page.

> If you are getting exceptions or errors regarding some missing services, try running the following command:

```shell
sudo php bin/clear-config-cache.php
```

> If `data/cache/config-cache.php` is present, that config will be loaded regardless of the `ConfigAggregator::ENABLE_CACHE` configuration in `config/autoload/mezzio.global.php`
