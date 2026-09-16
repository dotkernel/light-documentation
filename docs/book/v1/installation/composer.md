# Composer Installation of Packages

Composer is required to install Dotkernel Light. You can install Composer from the [official site](https://getcomposer.org/).

> First make sure that you have navigated your command prompt to the folder where you copied the files in the previous step.

## Install dependencies

Run this command in the command prompt.

> Use the **CLI** in order to ensure interactivity for proper configuration.

```shell
composer install
```

Composer resolves the dependency tree, writes a lock file and installs the packages into the `vendor` folder.
The run starts with a notice like this one:

```shell
No composer.lock file present. Updating dependencies to latest instead of installing from lock file. See https://getcomposer.org/install for more information.
```

The exact package count depends on the release you are installing, so do not be concerned if the number on your terminal differs from anyone else's.

The setup script may prompt for some configuration settings, for example the lines below.
If you don't see them, you can skip to the next section.

```shell
Please select which config file you wish to inject 'Laminas\HttpHandlerRunner\ConfigProvider' into:
  [0] Do not inject
  [1] config/config.php
  Make your selection (default is 1):
```

Type `0` to select `[0] Do not inject`.

> We choose `0` because Dotkernel includes its own ConfigProvider which already contains the prompted configurations.
> If you choose `[1] config/config.php`, an extra `ConfigProvider` will be injected.

The next question is:

`Remember this option for other packages of the same type? (y/N)`

Type `y` here, and hit `enter` to complete this stage.
