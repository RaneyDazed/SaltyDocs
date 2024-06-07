---
hide:
  - tags
tags:
  - logs
  - logging
---

# Apps

## Autoscan

### Check Status

```shell
docker ps | grep autoscan
```

### Restart Container

```shell
docker restart autoscan
```

### Previous Activity

```shell
cat /opt/autoscan/activity.log
```

### Live Log

```shell
tail -F /opt/autoscan/activity.log
```

## Cloudplow

### Check Status

```shell
sudo systemctl status cloudplow.service
```

### Previous Activity

```shell
cat /opt/cloudplow/cloudplow.log
```

Older logs are named as cloudplow.log.1, cloudplow.log.2, etc.

### Live Log

```shell
tail -F /opt/cloudplow/cloudplow.log
```

or

```shell
sudo journalctl -o cat -fu cloudplow.service
```

Sometimes, debug-level logging can be useful.  To enable this, make this change in the service file and restart the service.

In this file: `/etc/systemd/system/cloudplow.service`, change the log level to "DEBUG":

```text
...
WorkingDirectory=/opt/cloudplow/
ExecStart=/usr/bin/python3 /opt/cloudplow/cloudplow.py run --loglevel=DEBUG  <<<<< RIGHT THERE
ExecStopPost=/bin/rm -rf /opt/cloudplow/locks
Restart=always
...
```

You should only enable debug logging while you need it to track down a problem.

## Remote Mount

Pick one of these.

## Rclone VFS

### Check Status

The services that saltbox creates are named with this pattern: `saltbox_managed_rclone_nameofremote.service`; and in these examples are referred to as `SERVICE_FILE.service`. `nameofremote` is the name defined in the `remotes` section of `settings.yml`.

```shell
sudo systemctl status SERVICE_FILE.service
```

### See a live log

```shell
sudo journalctl -o cat -fu SERVICE_FILE.service
```

## Union Mount

### Check Status

```shell
sudo systemctl status mergerfs.service
```

### See a live log

```shell
sudo journalctl -o cat -fu mergerfs.service
```

## Docker

Find the container name: `docker ps -a`

## Live logs

### Live log (from the beginning of the log)

```shell
docker logs --follow <container_name>
```

### Live log (from the last 10 lines of the log)

```shell
docker logs --follow --tail 10 <container_name>
```

### Examples

```shell
docker logs -f plex
```

Note: `--follow` = `-f`
