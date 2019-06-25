# Tags Plugin

Plugin name: `tags`

The tags plugin adds the ability for HepBoat to respond with a custom message to a configured tag name.  

A tag can also be called directly with its name and the guild prefix (e.g. `!mytag`).

## Commands <a id="commands"></a>

| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!tags add {name} {content}` OR `!tags create {name} {content}` | Create a tag. | Trusted | `!tags add yes Yes hello friend` OR `!tags create wow oh yes` |
| `!tags show {name}` OR `!tags {name}` OR `!tag {name}` | Call a tag. | Trusted | `!tags show popcorn`   OR `!tags popcorn` |
| `!tags edit {name} {new content}` | Edit content of existing tag. | Moderator | `!tags edit owo More OWO!` |
| `!tags remove {name}` OR `!tags rm {name}` OR `!tags del {name}` | Remove tag by name. | Trusted | `!tags remove popcorn` |
| `!tags info {name}` | Get detailed info on a tag. | Trusted | `!tags info popcorn` |
| `!tags all` | List all tags in the server. | Trusted | `!tags all` |

### Tag Flags
When calling a tag using its short name (e.g. `!mytag`), you may add the following arguments in any combination.

| Flag | Description | Arg Type | Usage |
| :--- | :--- | :--- |  :--- |
| -c | Send the tag into another channel. | snowflake or mention | `!owo -c 532576772164812820` OR `!owo -c #chat` |
| -u | Mention a certain user when returning contents. | snowflake or mention | `!owo -u 148359099782791168` OR `!owo -u @JakeyPrime` |

### Tag Content Tokens
The following tokens can be used in tag contents to dynamically generate content when a tag is called.

| Token | Description |
| :--- | :--- |
| {user} | Will mention the calling user. |
| {server} | Will include the server name. |
| {channel} | Will mention the current channel. |
| {r&lt;snowflake&gt;} | Will mention the specified role. |
| {c&lt;snowflake&gt;} | Will mention the specified channel. |
| {u&lt;snowflake&gt;} | Will mention the specified user. |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| max_tag_length | Maximum length for a tag. | int | empty |
| min_level_remove_others | Minimum level for a user to delete another user's tags. | int | 50 |

## Configuration Example

```yaml
plugin:
  tags:
    max_tag_length: 100
    min_level_remove_others: 55
```

## Hardening

Tag calls and commands can be hardened by using the [Commands Plugin](commands-plugin.md). 

In overrides, the following special names are available.

| Name | Description |
| :--- | :--- | 
| `tags-usr`| Users that can trigger tag calls. |
| `tags-usr-allowed-roles`| Allows roles to run tags anywhere regardless of other override or lockdown settings. |

The hierarchy of overrides for tags calls is
```txt
1. tag-usr-allowed-roles
2. tag.name
3. tag-usr
```
meaning that the overrides for a specific tag.name trigger will override the overrides for `tag-usr`.

In lockdown, the following special name is available.

| Name | Description |
| :--- | :--- | 
| `tags-usr`| Users that can trigger tag calls. |

An example of a hardened configuration:

```yaml
commands:
  overrides:
  - name: mytag
    out:
      level: 10
  - name: tags-usr
    out:
      level: 50
  - plugin.name: tags
    out:
      level: 100
  lockdown:
  - name: tags-usr
    out:
      channels: [532709830767542303]  # chat
```

The above configuration sets the following:
* allows tag commands (e.g. `!tags edit`) to be only called by users level 100 or higher
* allows `!mytag` to be called by users level 10 or higher ONLY in channel `#chat`.
* allows all other tag calls (e.g. `!othertag`) to be called by users level 50 or higher ONLY in channel `#chat`.

