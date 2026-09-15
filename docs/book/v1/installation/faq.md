# Frequently Asked Questions

## How do I fix common permission issues?

If running your project you encounter some permission issues, follow the below steps.

### Errors

> PHP Fatal error:  Uncaught InvalidArgumentException: The directory "/var/www/_example.local_/html/data" is not writable...

> PHP Fatal error:  Uncaught InvalidArgumentException: The directory "/var/www/_example.local_/html/data/cache" is not writable...

**Fix:** give the web-server user write access through the group, rather than opening the folder to everyone.

```shell
sudo chown -R "$USER":www-data data
sudo chmod -R 775 data
```

### Error

> PHP Fatal error:  Uncaught ErrorException: fopen(/var/www/_example.local_/config/autoload/../../log/error-log-_yyyy-mm-dd.log_): Failed to open stream: Permission denied...

**Fix:**

```shell
sudo chown -R "$USER":www-data log
sudo chmod -R 775 log
```

> Replace `www-data` with the user your web server runs as if it differs — it is `apache` on AlmaLinux and RHEL derivatives, and `nginx` where nginx runs the worker processes.

> `chmod -R 777` is sometimes suggested for these folders.
> Avoid it outside a throwaway local VM: it lets anything on the machine rewrite the Twig and config caches, and those are executable PHP.
