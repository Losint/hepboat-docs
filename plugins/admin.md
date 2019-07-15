# Admin Plugin

Plugin name: `admin`

The admin plugin provides a set of administrator commands that help in moderating active servers.

## Commands

Arguments in `{}` are required. Arguments in `[]` are optional.

### Roles
| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!join {role}` OR `!add {role}` OR `!give {role}` | Assigns a role to the calling user. Role must be listed in `group_roles` in the config. | Default | `!join PC` OR `!add Console` OR `!give Tabletop` |
| `!leave {role}` OR `!remove {role}` OR `!take {role}` | Removes a role from the calling user. Role must be listed in `group_roles` in the config. | Default | `!leave PC` OR `!remove Console` OR `!take Tabletop` |
| `!role add {user} {role} [reason]` | Adds a role to a user. | Moderator | `!role add 232921983317180416 Moderator Promotion from Member` OR `!role add rowboat#0001 Admin Pretty good Moderator` |
| `!role remove {user} {role} [reason]` | Removes a role from a user .| Moderator | `!role remove 232921983317180416 Administrator Demoted for being bad at job` OR `!role remove rowboat#0001 Mod Terrible moderator` |
| `!role unlock {role}` | Unlocks a role listed in the `locked_roles` config setting for 5 minutes, allowing for permission updates. | Administrator | `!role unlock 346471724126044160` |
| `!role spray {role} [reason]` | Assigns the given role to all users in the guild. | Administrator | `!role spray 346471724126044160` |
| `!role nuke {role} [reason]` | Removes the given role from all users in the guild. | Administrator | `!role nuke 346471724126044160` |
| `!roles [query]` | Returns a list of IDs and names for all roles on the server or for roles that match the given query. A `[M]` tag is added for mentionable roles. Useful for configuring other plugins. | Moderator | `!roles` OR `!roles hepboat`|
| `!roleinfo {role}` | Display details about a role. | Moderator | `!roleinfo  274266640403791873` |
| `!tracking` | Displays number of members of roles in `tracking` config. | Moderator | `!tracking` |
| `!mention {role_id} {message}` OR `!mention here {role_id} {message}` | Posts a message in the current channel that will mention the given role where the token `{role}` is located. Will not work on roles that are already mentionable. | Moderator | `!mention 580569953065893899 {role}, here!`|
| `!mention channel {channel} {role_id} {message}` | Posts a message in the given channel that will mention the given role where the token `{role}` is located. Will not work on roles that are already mentionable. | Moderator | `!mention channel #chat 580569953065893899 {role}, here!`|
| `!mention enable {role_id}` OR `!mention disable {role_id}`|  Will enable or disable mention ability for the given role. | Moderator | `!mention enable 580569953065893899`|

#### Role Mention Message Tokens
The following tokens can be used in mention messages to dynamically generate content.

| Token | Description |
| :--- | :--- |
| {user} | Will mention the calling user. |
| {role} | Will mention the mentioned role. |
| {server} | Will include the server name. |
| {channel} | Will mention the current channel. |
| {r&lt;snowflake&gt;} | Will mention the specified role. |
| {c&lt;snowflake&gt;} | Will mention the specified channel. |
| {u&lt;snowflake&gt;} | Will mention the specified user. |

### Channels
| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!archive all [count]` OR `!archive here [count]`| Archives the latest `count` messages in the current channel. Default `count` value is 50. | Administrator | `!archive all 50` OR `!archive here 50` |
| `!archive user {user} [count]` | Archives the latest `count` messages from a given user in the guild. Default `count` value is 50. | Administrator | `!archive user 232921983317180416 100` OR `!archive user @rowboat#0001 100` |
| `!archive channel {channel} [count]` | Archives the latest `count` messages in the given channel. | Administrator | `!archive channel 289482554250100736 20` |
| `!clean all [count]` OR `!clear [count]` | Cleans the latest `count` messages in the current channel. Only works for messages that are sent after Hepboat has joined the channel. Default `count` value is 25. | Moderator | `!clean all 20` OR `!clear 20`|
| `!clean user {user} [count]` | Cleans the latest `count` messages from a given user in the current channel. Only works for messages that are sent after Hepboat has joined the channel. Default `count` value is 25. | Moderator | `!clean user 232921983317180416 50` |
| `!clean bots [count]` | Cleans the latest `count` messages sent by bots in the current channel. Only works for messages that are sent after Hepboat has joined the channel. | Moderator | `!clean bots 30` |
| `!nuke [count]` OR `!nuke here [count]` | Nukes the latest `count` messages in the current channel. Default `count` value is 10,000. | Administrator | `!nuke 20` OR `!nuke here 20`|
| `!nuke channel {channel} [count]` | Nukes the latest `count` messages from a given channel. Default `count` value is 10,0000. | Administrator | `!nuke channel 580894715705294869` |
| `!clean cancel` | Cancels any `clean` or `nuke` commands running in current channel. | Moderator | `!clean cancel` |
| `!cease` OR `!cease channel`| Remove send message permissions for `@everyone` in the current channel. | Moderator | `!cease` |
| `!uncease` OR `!uncease channel`| Restore send message permissions for `@everyone` in the current channel to the default. | Moderator | `!uncease` |
| `!shut` | Restricts the speak and use voice activation permissions for `@everyone` in the current voice channel of calling user. (Due to a Discord bug, this does not immediately mute everyone, but forces everyone to Push-to-Talk) | Moderator | `!shut` |
| `!unshut` | Removes restrictions for `@everyone` on speak and voice activation detection in the current voice channel of calling user. | Moderator | `!unshut` |
| `!slowmode {duration} [reason]` OR `!slowmode here {duration} [reason]` | Sets the slowmode time in the current channel. A duration of `0` will turn off slowmode in the channel. Given integer durations are parsed in minutes.| Moderator | `!slowmode 10` OR `!slowmode 5h` |
| `!slowmode channel {duration} [reason]` | Sets the slowmode time in the given channel. A duration of `0` will turn off slowmode in the channel. Given integer durations are parsed in minutes.| Moderator | `!slowmode channel 289482554250100736 10` OR `!slowmode channel 289482554250100736 5h` |

`archive` command results will be DMed to the calling user or linked in the chat based on `archive_link_chat` config setting. Archive results will also include deleted messages.

`clean` command archives will be linked in the modlogs under `MESSAGE_DELETE_BULK` if configured.

### User
| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!reactions clean {user} [count] [emoji]` | Removes the latest `count` of `emoji` reactions from a given user. Default `count` value is 10. If `emoji` is not set, it will remove all reactions by the given user.| Moderator | `!reactions clean 232921983317180416` OR `!reactions clean @rowboat#0001 30` OR `!reactions clean 232921983317180416 20 :thinking:` |
| `!backups restore {user}` | Restores a user to the most recently saved member backup. | Administrator | `!backups restore 232921983317180416` OR `!backups restore rowboat#0001` |
| `!backups clear {user}` | Deletes all saved backups for a user. | Administrator | `!backups clear 232921983317180416` OR `!backups clear rowboat#0001` |
| `!stats {user}` | Presents general message statistics for a given user. | Moderator | `!stats 232921983317180416` OR `!stats rowboat#0001` |
| `!voice log {user}` | Displays all recent voice channel activity for a given user in guild. | Moderator | `!voice log 232921983317180416` OR `!voice log @rowboat#0001` |
| `!nick change {user} {nickname}` OR `!nick add {user} {nickname}` | Adds or changes a nickname for the given user. Will also check the censor config if set. | Moderator | `!nick change 84912325282254848 newnick` OR `!nick add @Jakey newnick` |
| `!nick remove {user}` OR `!nick rmv {user}` OR `!nick delete {user}` OR `!nick del {user}` | Removes a nickname from the given user. | Moderator | `!nick remove 84912325282254848 newnick` OR `!nick rmv @Jakey` |

### Server
| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!emojistats {server/global} {least/most}` | Displays the least/most used emojis in the current guild/globally. | Moderator | `!emojistats global most` OR `!emojistats server least` |
| `!invites prune [count]` | Deletes server invites with `count` uses or less. Default `count` value is 1. | Administrator | `!invites prune 5` |
| `!cease guild` | Remove send message permissions for @everyone in the guild. | Moderator | `!cease guild` |
| `!uncease guild` | Restore send message permissions for @everyone in the guild to the default. | Moderator | `!uncease guild` |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| archive_link_chat | Archive links will be sent in channel if true or DMs if false. | bool | false
| persist | A single member persistence configuration. | dict | empty |
| role_aliases | Mapping of strings to role IDs. Alias strings can be used in place of IDs in commands. | dict | empty |
| group_roles | Mapping of strings to role IDs of roles which can be joined and left by any user by command. These roles cannot grant any elevated permissions. | dict | empty |
| group_confirm_reactions | Add a confirmation reaction for user role joins. | bool | false |
| locked_roles | List of roles that may not have any permissions changed unless unlocked by command. | list(snowflake) | empty |
| tracking | List of roles that can be tracked with the `tracking` command. | list(snowflake) | empty |
| confirm\_actions | Confirm when actions are performed | bool | true |
| mobile\_mod\_channel | Channel to send any mobile modding dialog. | snowflake | empty |
| onjoin\_roles | List of roles automatically added to any new guild user. | list(snowflake) | empty |
| welcomes | Mapping of channel IDs to welcome configurations. | dict | empty |

### Member Persistence Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| roles | Whether to recover roles when a user rejoins the server. | bool | false |
| role_ids | A list of role IDs which will be recovered if `roles` is true. | list(snowflake) | empty |
| nickname | Whether to recover the nickname when a user rejoins the server. | bool | false |
| voice | Whether to recover mute/deafen settings when a user rejoins the server. | bool | false |

### Welcome Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| msg | Message that will be sent to the channel when a member joins the guild | str | empty |
| dm | Whether the message should also be sent as a DM. | bool | False |

#### Message Tokens

| Token | Description |
| :--- | :--- |
| {user} | Will mention the joining user. |
| {server} | Will include the server name. |
| {channel} | Will mention the current channel. |
| {r&lt;snowflake&gt;} | Will mention the specified role. |
| {c&lt;snowflake&gt;} | Will mention the specified channel. |
| {u&lt;snowflake&gt;} | Will mention the specified user. |

## Configuration Example

```yaml
plugins:
  admin:
    persist:
      roles: true
      role_ids: [278810978722906112, 278972423502561280, 278972377587515392]
      nickname: true
      voice: false
    role_aliases:
      role1: 205769314199011329
      role2: 333806119199703042
    group_roles:
      PC: 278810978722906112
      Console: 278972377587515392
      Tabletop: 278972423502561280
    locked_roles: [346471724126044160, 252184905075654657]
    tracking: [346471724126044160, 252184905075654657]
    welcomes:
      238947029384908908234:
        msg: |-
          Welcome to the {server}, we've got fun and games, {user}.
          Please read {c29837890467823647978} for more info.
          You have joined {channel}!
        dm: false
      00000000000000000000:
        msg: |-
          Hello {user}! Welcome to the {server}. Don't forget to check out {c238947029384908908234}
        dm: true
```

