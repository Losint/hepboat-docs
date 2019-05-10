# Tags Plugin

The tags plugin allows the ability to provide a custom command response to a set command.  
A tag can also be run directly with its name and the guild prefix such as `!mytag`

#### 

## Commands <a id="commands"></a>

| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!tags create` | Adds a warning infraction to a user | Trusted | `!tags add yes yes` OR `!tags create wow oh yes` |
| `!tags show {tag}` | Get the content of a tag | Trusted | `!tags show popcorn`   OR `!tags popcorn` |
| `!tags remove {tag}` | Remove tag by name | Trusted | `!tags remove popcorn` |
| `!tags info {tag}` | Get information on a tag | Trusted | `!tags info popcorn` |
| `!tags all` | List all tags for the server | Trusted | `!tags all` |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| max\_tag\_length | Maximum length for a tag | int | \* |
| max\_level\_remove\_others | Minimum level required to remove someone else's tag | int | 50 |

## Configuration Example

```yaml
  tags:
    max_tag_length: 100
    min_level_remove_others: 55
```

## Hardening Example

Tags can be hardened by using the Commands Plugin option for overrides and lockdown. 

The name `tags-usr` can be defined to specify all created tags running directly.

The name `mytag` can be defined to specify a specific created tag.

 An example of a hardened configuration is as follows
```yaml
commands:
  overrides:
  - name: tags-usr
    out:
      level: 100
  - plugin.name: tags
    out:
      level: 100
  lockdown:
  - name: tags-usr
    out:
      channels: [384869993789128704]
```

If you want to leak channels you can leak the name as the override or lockdown such as below

```yaml
commands:
  overrides:
  - name: tags-usr
    out:
      level: 100
  - name: mytag
    out:
      level: 0
  - plugin.name: tags
    out:
      level: 100
  lockdown:
  - name: tags-usr
    out:
      channels: [384869993789128704]
  - name: mytag
    out:
      channels: [987230980342345423]
```

