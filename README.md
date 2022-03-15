## foreman-proxy

### Build image

```
docker-compose build salt-with-foreman-proxy
```

### Start foreman-proxy

```
docker-compose run --rm --entrypoint /usr/share/foreman-proxy/bin/smart-proxy salt-with-foreman-proxy --no-daemonize
```

### Error message

```
2022-03-15T13:06:43  [E] Couldn't enable 'dynflow'
2022-03-15T13:06:43  [W] Error details for Couldn't enable 'dynflow': <Sequel::DatabaseConnectionError>: SQLite3::CantOpenException: unable to open database file
```

### Workaround

Uncomment mount in `docker-compose.yml` to fix the database path

```
- ./etc_master/foreman-proxy/settings.d/dynflow.yml:/etc/foreman-proxy/settings.d/dynflow.yml
```

Run again

```
docker-compose run --rm --entrypoint /usr/share/foreman-proxy/bin/smart-proxy salt-with-foreman-proxy --no-daemonize
```
