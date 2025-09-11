# Running the application

We recommend running the application on **AlmaLinux 10**, using **WSL 2**:

- if you don't already have:
    - install [WSL 2](https://docs.dotkernel.org/development/v2/setup/system-requirements/)
    - install [AlmaLinux 10](https://docs.dotkernel.org/development/v2/setup/installation/)
- install the application in a virtualhost as recommended by the chosen distro
- set `$baseUrl` in **config/autoload/local.php** to the address of the virtualhost
- set the permissions for the `data` folder

```shell
chmod -R 777 ./data
```

- set the permissions for the log folder

```shell
chmod -R 777 ./log
```

- run the application by opening the virtualhost address in your browser

You should see the `Dotkernel Light` welcome page.

> If you are getting exceptions or errors regarding some missing services, try running the following command:

```shell
sudo php ./bin/clear-config-cache.php
```

> If `data/cache/config-cache.php` is present, that config will be loaded regardless of the `ConfigAggregator::ENABLE_CACHE` configuration in `config/autoload/mezzio.global.php`
