# Clone the project

## Summary

How to get a local copy of Dotkernel Light onto your machine, either with the recommended one-step Composer command or by cloning the repository directly.

## Recommended development environment

> If you are using Windows as OS on your machine, you can use WSL2 as development environment.
>
> Currently we provide a distro implementation for [AlmaLinux 10](https://docs.dotkernel.org/development/v2/setup/installation/).

## Installing Dotkernel Light

The recommended way to install Dotkernel Light is a single Composer command, which creates the directory, installs dependencies, and enables development mode in one step:

```shell
composer create-project dotkernel/light dk
cd dk
```

### Cloning the repository directly

If you are instead cloning the repository directly — for example to contribute to Dotkernel Light itself — navigate inside the directory you want to download the project files into.

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

Continue with [Composer Installation](composer.md), which requires the extra manual `composer development-enable` step that `composer create-project` performs for you automatically.

You can already open the project in your preferred IDE to double-check the files were copied correctly.

## FAQ

**Q: What is the fastest way to install Dotkernel Light?**
A: `composer create-project dotkernel/light dk` — it creates the directory, installs dependencies, and enables development mode in one step.

**Q: Do I need an empty directory for `composer create-project`?**
A: No — only the manual `git clone` path requires an empty, writable directory.

**Q: If I clone the repository directly, what extra step do I need that `composer create-project` skips?**
A: Running `composer development-enable` yourself, since only `composer create-project` runs it automatically.
