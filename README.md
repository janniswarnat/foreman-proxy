## foreman-proxy

### Build image

```
docker-compose build salt-with-foreman-proxy
```

### Start foreman-proxy

```
docker-compose run --rm --entrypoint /usr/share/foreman-proxy/bin/smart-proxy salt-with-foreman-proxy --no-daemonize
```

### Reproduce issue

Comment mount in `docker-compose.yml`

```
#      - ./etc_master/foreman-proxy/settings.d/dynflow.yml:/etc/foreman-proxy/settings.d/dynflow.ym
```

and run again

```
docker-compose run --rm --entrypoint /usr/share/foreman-proxy/bin/smart-proxy salt-with-foreman-proxy --no-daemonize
```
