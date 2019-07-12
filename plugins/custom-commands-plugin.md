# Custom Commands Plugin

Plugin name: `custcommands`

The custom commands plugin allows guild admins a way to create custom commands that allow multiple actions to be performed when the required trigger is done. This can be defined as an in chat command or by waiting for specific actions to occur such as a message containing a specific string.  

All commands in the custom commands plugin are configured to `ADMIN` \(level 100\) by default due to how sensitive the commands can be. Incorrectly creating commands **can** allow privileged access where it was not intended. There is no permissions checking when creating or running any of these commands. For example, if you create a command that grants admin access, it will grant admin access to ANYONE who is able to trigger this by default.

The hardening section shows a recommended configuration that will lock down created custom commands to a specific admin channel so they can be individually leaked into user channels.

The [infractions plugin](infractions.md) should also be enabled and set up in order to use most of the punishment custom command options. Custom commands can also use `role_aliases` set up in the [admin plugin](admin.md).

## Commands

Arguments in `{}` are required. Arguments in `[]` are optional.

| Name | Description | Usage |
| :--- | :--- | :--- |
| `!cc all` OR `!cc list` | Displays all defined custom commands | `!cc all` |
| `!cc info {name}` | Display information about the given custom command | `!cc info kittens` |
| `!cc delete {name}` OR `!cc del {name}` OR `!cc remove {name}` OR `!cc rm {name}` | Deletes the given custom command | `!cc delete kittens` |
| <code>!cc create {name} {type} {listen_type} &lt;command1&gt; &#124; &lt;command2&gt;</code> OR <code>!cc add {name} {type} {listen_type} &lt;command1&gt; &#124; &lt;command2&gt;</code>| Creates a custom command with defined attributes. | <code>!cc create testing cmd 0 notify  &#124; addgroup cats &#124; addgrouptemp dogs 20m</code> |

### Creation Options
Arguments in `{}` are required. Arguments in `[]` are optional.

#### `type` Options
| Name | Description |
| :--- | :--- |
| cmd | A command that is triggered by running the command name in a channel .<br/><br/> e.g. `!showmecats` will execute the commands contained within the `showmecats` command. | 
| listen | A command that is automatically executed based on trigger options. <br/><br/> e.g. `!cc create listen MessageCreate reply cats I like cats, too!` will respond to any message with the string `cats` with `I like cats, too!` |
 
#### `listen_type` Options

For `cmd` custom command types:

| Name | Info |
| :--- | :--- |
| 0 | Technically, anything can be defined for the Listen Type, but `0` is a common placeholder. |

For `listen` custom command types:

| Name | Info |
| :--- | :--- |
| MessageCreate | The custom command is triggered when a message is created and a specific defined trigger option is performed. |

#### `cmd`-type Options

| Command | Info | Usage |
| :--- | :--- | :--- |
| `allowargs` | *Should be defined prior to other commands if used.* Enables other commands defined after this command to accept overriding `user` and `reason` arguments when the custom command is called. Otherwise, the commands will be applied to the calling user by default. | `allowargs` |
| `notify` | *Should be defined prior to other commands if used.* Enables a confirmation response of successful commands defined after this command. | `notify` |
| `addgroup {role}` | Adds the given role to the user. | `addgroup 580569861764284417` OR `addgroup member` OR `addgroup @member` |
| `removegroup {role}` | Removes the given role from the user. | `removegroup 580569861764284417` OR `removegroup member` OR `removegroup @member` |
| `addgrouptemp {role} {duration} [reason]` | Adds the given role temporarily for the given duration to the user. | `addgrouptemp 580569861764284417 1m` OR `addgrouptemp member 10s here's a reason` OR `addgrouptemp @member 1h` |
| `kick [reason]` | Kicks the user from the guild. | `kick` OR `kick bad temper` |  
| `tempban {duration} [reason]` | Temporarily bans the user for the given duration. | `tempban 1m` |
| `softban [reason]` | Softbans (bans/unbans) a user and deletes any of their messages that were sent within the last 7 days. | `softban` OR `softban bad temper` |
| `ban [reason]` | Bans a user from the guild. | `ban` |
| `warn [reason]` | Adds a warning infraction to a user. | `warn just because` |
| `mute [reason]` | Mutes a user. `mute_role` must be set in the `infractions` config. | `mute` |
| `mutehard [reason]` | Hard-mutes a user. `hard_mute_role` must be set in the `infractions` config. | `mutehard` |
| `tempmute {duration} [reason]` |  Temporarily mutes a user. `mute_role` must be set in the `infractions` config. | `tempmute 5h` |
| `tempmutehard {duration} [reason]` | Temporarily hard-mutes a user. `hard_mute_role` must be set in the `infractions` config. | `tempmutehard 2m` |
| `mutevc [reason]` | Moves a voice user to a guild-defined AFK channel. | `mutevc` | 

#### `listen`-type Options

##### `MessageCreate` Options

| Command | Info | Usage |
| :--- | :--- | :--- |
| `reactall {channel_id} {emoji}` | Will react to every user message in the defined channel with the emoji. | `reactall 579304983896391682 :rabbit:` OR `reactall 579304983896391682 hydra:582615263422447637` OR `reactall 579304983896391682 <:hydra:582615263422447637>`|
| `replyall {channel_id} {reply_str}` | Will reply to every user message in the defined channel with `reply_str`. | `replyall 579304983896391682 OK` |
| `react {search_str} {emoji}` | Will naively react to all instances of `search_str` with the emoji. This includes commands with the `search_str`. `search_str` can be multiple words, if surrounded by single quotes. | `react cat :cat:` OR `react 'good morning' :sunny:` | 
| `reply {search_str} {reply_str}` | Will react to all instances of `search_str` with `reply_str`. `search_str` can be multiple words, if surrounded by single quotes. | `reply cat dog` OR `reply 'good morning' good night!` |
| `reactcmd {cmd_str} {emoji}` | Will react to all instances of `!cmd_str` with the emoji. `cmd_str` can be multiple words, if surrounded by single quotes. | `reactcmd 'tags owo' :rabbit:` |
| `replycmd {cmd_str} {reply_str}` | Will reply to all instances of `!cmd_str` with the reply message. `cmd_str` can be multiple words, if surrounded by single quotes. | `replycmd 'tags owo' BUNNY~` |

##### `reply_str` Tokens
The following tokens can be used in `reply_str` contents to dynamically generate content when a `listen`-type custom command is triggers.

| Token | Description |
| :--- | :--- |
| {user} | Will mention the calling user. |
| {server} | Will include the server name. |
| {channel} | Will mention the current channel. |
| {r&lt;snowflake&gt;} | Will mention the specified role. |
| {c&lt;snowflake&gt;} | Will mention the specified channel. |
| {u&lt;snowflake&gt;} | Will mention the specified user. |

### Creation Examples

Create a custom command named `react_hydra` that listens to all messages and reacts to the string `ssss` with the `hydra:582615263422447637` emoji:
```text
!!cc create react_hydra listen messagecreate react ssss hydra:582615263422447637
```

Create a custom command named `cmd_owo_reply` that listens to all `!owo` commands and responds with the string `@owo_author :rabbit:`.
```text
!!cc create cmd_owo_reply listen MessageCreate replycmd owo {user} :rabbit:
```

Create a custom command named `tempgroup_reason`. When triggered using the command  `!tempgroup_reason {user}`, temporarily add the role `@blah` to `user` for 5 seconds with the reason "you're the best" and confirm the role addition with a response.
```text
!!cc create tempgroup_reason cmd 0 notify|allowargs|addgrouptemp @blah 5s you're the best
```

Create a custom command named `roles_setup`. When triggered using the command `!roles_setup`, the calling user will have the role with id `580897510780960768` temporarily added for 1 minute, have the role `@a` added, and the role `b` removed. HepBoat will confirm each role modification with a distinct response.
```text
!!cc create roles_setup  cmd 0 notify|addgrouptemp 580897510780960768 1m|addgroup a|removegroup b
```

## Configuration Example

```yaml
plugins:
  custcommands: {}
  infractions:
    mute_role: 579398816072073246
```

## Hardening

The following configuration is a recommended basic guild level configuration to harden the custom commands plugin.

```yaml
commands:
  overrides:
  - name: cc-usr
    out:
      level: 100
  lockdown:
  - group: cc
    out:
      channels: [504782681263964162] # Admin commands channel
  - name: cc-usr
    out:
      channels: [504782681263964162] # Admin commands channel
```

The configuration above allows only admin-level users to call any `!cc` group and trigger `cmd` type custom commands in only the admin commands channel. 

The special `cc-usr` command name applies to all `cmd` type custom commands. It is recommended to set this to a high level (at least moderator) as otherwise by default any create `cmd` type custom commands can be run by any user.

### `cmd`-type Hardening

If you would like to leak certain `cmd` type custom commands to different levels and channels, you can override each command individually. For instance, in the following example, if you would like to leak the `role_jokes` custom command to be used by any user in the user commands channel:

```yaml
commands:
  overrides:
  - name: cc-usr
    out:
      level: 100
  - name: role_jokes
    out:
      level: 0
  lockdown:
  - group: cc
    out:
      channels: [504782681263964162] # Admin commands channel
  - name: cc-usr
    out:
      channels: [504782681263964162] # Admin commands channel
  - name: role_jokes
    out:
      channels: [504782681263964123] # User commands channel
```

### `listen`-type Hardening

If you would like to restrict certain `listen`-type custom commands to certain channels or role triggers, you can override them by custom command name individually in the `lockdown` configuration. For instance, in the following example, if you would like only the `member` role to trigger the `reply_hello` `listen`-type custom commands in the #general channel: 

```yaml
commands:
  overrides:
  - name: cc-usr
    out:
      level: 100
  lockdown:
  - group: cc
    out:
      channels: [504782681263964162] # Admin commands channel
  - name: cc-usr
    out:
      channels: [504782681263964162] # Admin commands channel
  - name: reply_hello
    out:
      channels: 
       - 580894715705294869 # #general channel
      roles:
       - 580897510780960768 # member role
```

