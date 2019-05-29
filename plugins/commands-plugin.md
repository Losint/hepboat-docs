---
description: >-
  Controls usage of commands by level, channel, etc. There is a special case for
  the name, which controls all tag usage.
---

# Commands Plugin

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| lockdown | A mapping of commands and channels to whitelist | dict | empty |
| prefix | A mapping of channels to Censor Configurations | dict | empty |
| overrides | Command overrides  | dict | empty |
| exclude\_msg\_user | Ignore logging for users | snowflake list | empty |
| dm\_denied | Whether or not to DM a user when their command is denied | bool | True |
| local\_blacklist | A list of users ignored from using the bot on this server. | list | empty |

## Lockdown Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| name | Name of the command to whitelist | string | empty |
| group | Command group to  whitelist | string | empty |
| plugin.name | Name of the plugin to whitelist | string | empty |
| out | Output options | dict | empty |
| out -&gt; channels | list of channels to whitelist | snowflake list | empty |
| out -&gt; category | list of channel categories to whitelist | snowflake list | empty |
| out -&gt; roles | list of roles to whitelist | snowflake list | empty |
| out -&gt; exclude\_channels | list of channels to blacklist | snowflake list | empty |
| out -&gt; exclude\_category | list of channel categories to blacklist | snowflake list | empty |
| out -&gt; roles | whitelisted roles | snowflake list | empty |

`name` allows for a command name, custom command/tag name, or `tags-usr` to represent the level for all tags.

`tags-usr-allowed-roles` allows specification for a role to be able to run tags in general

## Overrides Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| name | Name of the command to override | string | empty |
| group | Command group to  override | string | empty |
| plugin.name | Name of the plugin to override | string | empty |
| out | Output options | dict | empty |
| out -&gt; level | level to restrict command to | snowflake array | empty |



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
    - name: info
      out:
        level: 50
    - group: role
      out:
        level: 60
    lockdown:
    - name: info
      out:
        channels: 
          - 510415911560282132
          - 511870279157284874
    - group: infractions
      out:
        channels: 
          - 510415911560282132 
          - 511870279157284874
        category: [32498723498049874]
        roles: [9872389732498023409]
    - plugin.name: admin
      out:
        channels: 
          - 510415911560282132
          - 511870279157284874
    dm_denied: true
    local_blacklist:
      - 132256368353607681
      - 324841099090853888
```

