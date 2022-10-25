Clone this repo and change the volume path to match your own in docker-compose.yml

## Reproduction

### Setup

`id -u && id -g`:

```
501
20
```

My /etc/exports:

```
/Users/karl -alldirs -mapall=501:20
```

My /etc/nfs.conf:

```
nfs.server.mount.require_resv_port = 0
```

In one shell launch the container: `docker-compose up`

### Docker NFS
In another shell:

```
docker compose exec php php /var/www/app/small.php
```

Should print out "small"

```
docker compose exec php php /var/www/app/large.php
```

Should hang (or print out "large" if it works for you I guess).

### Plain NFS

On another Mac, mount that same directory over NFS.

`cat small.php` works, as does `cat large.php`.