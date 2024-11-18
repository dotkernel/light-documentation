# Clone the project

## Recommended development environment

> If you are using Windows as OS on your machine, you can use WSL2 as development environment.
>
> Read more on [dotkernel.com](https://www.dotkernel.com/php-development/almalinux-9-in-wsl2-install-php-apache-mariadb-composer-phpmyadmin/).

Using your terminal, navigate inside the directory you want to download the project files into.

> Make sure that
>
> - The directory is empty before proceeding to the download process.
>     - You will get this error if the directory is not empty `fatal: destination path '.' already exists and is not an empty directory.` and no files will be cloned.
> - That you have writing permissions on the directory.

Once there, run the following command:

```shell
git clone https://github.com/dotkernel/light.git .
```

If everything ran correctly, you can expect to see an output like this, though the numbers may differ.

```shell
Cloning into '.'...
remote: Enumerating objects: 500, done.
remote: Counting objects: 100% (500/500), done.
remote: Compressing objects: 100% (435/435), done.
remote: Total 500 (delta 51), reused 448 (delta 27), pack-reused 0 (from 0)
Receiving objects: 100% (500/500), 399.14 KiB | 3.91 MiB/s, done.
Resolving deltas: 100% (51/51), done.
```

You can already open the project in your preferred IDE to double-check the files were copied correctly.
