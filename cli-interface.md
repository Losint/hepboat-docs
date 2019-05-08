# CLI Interface

There is some functionality you have to enable via command line, such as adding a global admin or whitelisting servers.

#### Remove Guild Flags

```bash
docker-compose exec web ./manage.py wh-rmv GUILD_ID_HERE FLAG_HERE
```

#### Valid Guild Flags

| Option | Description |
| :--- | :--- |
| `MODLOG_CUSTOM_FORMAT` | Allows the modlog custom format |
| `MUSIC` | Does nothing |
| 'PREMIUM' | SOONTM | 