---
description: >-
  Controls usage of commands by level, channel, etc.
---

# Commands Plugin

Plugin name: `commands`

**Note that this plugin should *not* be under `plugins:` but in the main level configuration.**
See [General Configuration](general.md) for details.

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| prefix | The prefix to use for HepBoat commands in the server. | str | '' |
| overrides | A mapping of commands and override configurations.  | dict | empty |
| lockdown | A mapping of commands and channel lockdown configurations. | dict | empty |
| dm\_denied | DM a user when their command is denied. | bool | True |
| local\_blacklist | Blacklisted users that HepBoat will ignore all commands from. | list(snowflake) | empty |
| exclude\_msg\_user | Users that will not be logged by HepBoat. | list(snowflake) | empty |
| timezone | Timezone to use for localized timestamps in command outputs. [Supported timezones.](https://gist.github.com/heyalexej/8bf688fd67d7199be4a1682b3eec7568) | str | `UTC` |

## Overrides Configuration Options

Overrides are useful for overriding the default level permissions on commands. Level overrides are checked before any channel lockdowns for commands.

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| name | A command name (default, custom, or short tag) | string | empty |
| group | A command group name | string | empty |
| plugin.name | A plugin name | string | empty |
| out | Output options | dict | empty |
| out &rarr; level | Minimum level (inclusive) to use commands | int | 0 |
| out &rarr; disabled | *For command names only.* Disable the command entirely. | bool | False |

Command group names include commands that start with a common command. e.g. `group: tags` would include tags such as
`!tags add` and `!tags edit`.

Plugin names include commands that are located under a certain plugin. e.g. `plugin.name: utilities` would include all
its commands such as `!bunny` and `!emoji`. Please see individual plugin documentation for specific plugin names.

The hierarchy of overrides is
```txt
1. name
2. group
3. plugin.name
```
meaning that the overrides for a specific command name will override the overrides for a command group, etc.

### Special Overrides Command Names

| Command name | Description |
| :--- | :--- | 
| `cc-usr`| Users that can trigger custom command commands. |
| `cc-usr-allowed-roles`| Allows roles to run custom commands anywhere regardless of other override or lockdown settings. |
| `tags-usr`| Users that can trigger tag calls. |
| `tags-usr-allowed-roles`| Allows roles to run tags anywhere regardless of other override or lockdown settings. |

The hierarchy of overrides for custom command calls for example would be
```txt
1. cc-usr-allowed-roles
2. cc.name
3. cc-usr
```
meaning that the overrides for a specific custom command trigger will override the overrides for `cc-usr`.
  
Example configuration setup:
```yaml
commands:
  overrides:
    - name: tags-usr
      out:
        level: 10
    - name: tags-usr-allowed-roles
      out:
        roles:
          - 9872389732498023409
    - name: cc-usr
      out:
        level: 60
    - name: tags-cc-allowed-roles
      out:
        roles:
          - 9872389732498023409
```

## Lockdown Configuration Options

Lockdowns are useful for hardening commands to only work in certain channels, categories, and by certain roles. Lockdown configurations work together with default command levels and overrides configurations.

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| name | A command name (default, custom, or short tag) | string | empty |
| group | A command group | string | empty |
| plugin.name | A plugin name | string | empty |
| out | Output options | dict | empty |
| out &rarr; channels | Whitelisted channels | list(snowflake) | empty |
| out &rarr; category | Whitelisted categories | list(snowflake) | empty |
| out &rarr; roles | Whitelisted roles | list(snowflake) | empty |
| out &rarr; exclude\_channels | Blacklisted channels | list(snowflake) | empty |
| out &rarr; exclude\_category | Blacklisted channel categories | list(snowflake) | empty |

Blacklists are respected over whitelists in a conflict.

### Special Lockdown Command Names

| Command name | Description |
| :--- | :--- | 
| `cc-usr`| Users that can trigger custom command commands. |
| `tags-usr`| Users that can trigger tag calls. |

## Example configuration

```yaml
commands:
  prefix: '!'
  overrides:
    - name: tempmute
      out:
        level: 40
    - name: mute
      out:
        level: 40
    - group: role
      out:
        level: 60
    lockdown:
    - name: info
      out:
        channels: 
          - 510415911560282132  # Channel ID
          - 511870279157284874  # Channel ID
    - group: tags
      out:
        channels: 
          - 510415911560282132  # Channel ID
          - 511870279157284874  # Channel ID
        category:
          - 32498723498049874  # Category ID
        roles: 
          - 9872389732498023409  # Role ID
    - plugin.name: admin
      out:
        channels: 
          - 510415911560282132  # Channel ID
          - 511870279157284874  # Channel ID
  dm_denied: true
  local_blacklist:
    - 132256368353607681  # User ID
    - 324841099090853888  # User ID
```

