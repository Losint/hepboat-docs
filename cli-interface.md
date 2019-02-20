# CLI Interface

There is some functionality you have to enable via command line, such as adding a global admin or whitelisting servers.



### Add Global Admin

```bash
docker-compose exec web ./manage.py add-global-admin USER_ID_HERE
```



### Add Guild Flags

```bash
docker-compose exec web ./manage.py wh-add GUILD_ID_HERE FLAG_HERE
```

#### Remove Guild Flags

```bash
docker-compose exec web ./manage.py wh-rmv GUILD_ID_HERE FLAG_HERE
```

#### Valid Guild Flags

| Option | Description |
| :--- | :--- |
| `MODLOG_CUSTOM_FORMAT` | Allows the modlog custom format |
| `MUSIC` | Does nothing |