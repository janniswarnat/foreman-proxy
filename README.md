## foreman-proxy

### Build image

```
docker-compose build salt-with-foreman-proxy
```

### Start foreman-proxy

```
docker-compose run --rm --entrypoint /usr/share/foreman-proxy/bin/smart-proxy salt-with-foreman-proxy --no-daemonize
```

### Workaround

Uncomment mount in `docker-compose.yml` to fix the database path

```
- ./etc_master/foreman-proxy/settings.d/dynflow.yml:/etc/foreman-proxy/settings.d/dynflow.yml
```

and run again

```
docker-compose run --rm --entrypoint /usr/share/foreman-proxy/bin/smart-proxy salt-with-foreman-proxy --no-daemonize
```
