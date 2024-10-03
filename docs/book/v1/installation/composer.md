# Composer Installation of Packages

Composer is required to install DotKernel `Light`. You can install Composer starting [here](https://getcomposer.org/).

## Install dependencies

```shell
composer install
```

The setup script will prompt you for the below configuration setting:

```shell
Please select which config file you wish to inject 'Laminas\HttpHandlerRunner\ConfigProvider' into:
  [0] Do not inject
  [1] config/config.php
  Make your selection (default is 1):
```

Simply select `[0] Do not inject`, because DotKernel includes its own ConfigProvider which already contains the prompted configurations.

The next question is:

`Remember this option for other packages of the same type? (y/N)`

Type `y` here, and hit `Enter`.
