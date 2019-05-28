# Tags Plugin

The tags plugin allows the ability to provide a custom command response to a set command.  
A tag can also be run directly with its name and the guild prefix such as `!mytag`

#### 

## Commands <a id="commands"></a>

| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!tags create` | Creates a tag | Trusted | `!tags add yes Yes hello friend` OR `!tags create wow oh yes` |
| `!tags show {tag}` | Get the content of a tag and how many uses it has | Trusted | `!tags show popcorn`   OR `!tags popcorn` |
| `!tags edit {tag} {new content}` | Edit content of existing tag | Moderator | `!tags edit owo More OWO!` |
| `!tags remove {tag}` | Remove tag by name | Trusted | `!tags remove popcorn` |
| `!tags info {tag}` | Get information on a tag | Trusted | `!tags info popcorn` |
| `!tags all` | List all tags for the server | Trusted | `!tags all` |

## Tag Flags
| Flag(s) | Description | Usage |
| :--- | :--- | :--- |
| -c | Allows to send tag into another channel | !owo -c 532576772164812820 |
| -u | Allows to send tag in current channel but ping a certain user before it's contents. | !owo -u 148359099782791168 |
| -c -u | Allows to send tag in another channel and ping a member in the same tag | !owo -c 532576772164812820 -u 148359099782791168 |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| max\_tag\_length | Maximum length for a tag | int | \* |
| min\_level\_remove\_others | Minimum level required to remove someone else's tag | int | 50 |

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
      channels: [532709830767542303]
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
      channels: [532709830767542303]
  - name: mytag
    out:
      channels: [532709830767542303]
```

