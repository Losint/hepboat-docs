# Admin Plugin

The admin plugin provides a set of administrator commands that help in moderating active servers.

## Commands

| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!join / add / give {role}` | Assigns a role if it's listed in the group\_roles config setting | Default | `!join PC` OR `!add Console` OR `!give Tabletop` |
| `!leave / remove / take {role}` | Removes a group role from a user if it's listed in the group\_roles config setting| Default | `!leave PC` OR `!remove Console` OR `!take Tabletop` |
| `!temprole {user} {role ID} {duration} [reason]` | Temporarily applies a role to a user | Moderator | `!temprole 232921983317180416 295646805650046977 7d Trial Mod` OR `!temprole @rowboat#0001 295646805650046977 24h Member of the Day` |
| `!roles` | Returns a list of ids/names for all roles on the server. Useful for configuring other rowboat plugins | Moderator | `!roles` |
| `!role add {user} {role} [reason]` | Adds a role to a user | Moderator | `!role add 232921983317180416 Moderator Promotion from Member` OR `!role add rowboat#0001 Admin Pretty good Moderator` |
| `!role remove {user} {role} [reason]` | Removes a role from a user | Moderator | `!role remove 232921983317180416 Administrator Demoted for being bad at job` OR `!role remove rowboat#0001 Mod Terrible moderator` |
| `!role unlock {role ID}` | Unlocks a role listed in the locked\_roles config setting for 5 minutes, allowing permission updates | Administrator | `!role unlock 346471724126044160` |
| `!archive (here / all) [count]` | Archives \[count\] many messages in the current channel | Admin | `!archive all 50` OR `!archive here 50` |
| `!archive user {user} [count]` | Archives \[count\] many messages that a given user sent in the current guild | Admin | `!archive user 232921983317180416 100` OR `!archive user @rowboat#0001 100` |
| `!archive channel {channel} [count]` | Archives \[count\] many messages in the given channel | Admin | `!archive channel 289482554250100736 20` |
| `!clean all / clear [count]` | Cleans \(deletes\) \[count\] many messages in the current channel | Moderator | `!clean all 20` |
| `!clean user {user} [count]` | Cleans \[count\] many messages a given user sent in the current channel | Moderator | `!clean user 232921983317180416 50` |
| `!clean bots [count]` | Cleans \[count\] many messages sent by bots in the current channel | Moderator | `!clean bots 30` |
| `!clean cancel` | Cancels any cleaning process running in current channel | Moderator | `!clean cancel` |
| `!reactions clean {user} [count] [emoji]` | Removes the most recent count of reactions from a given user | Moderator | `!reactions clean 232921983317180416` OR `!reactions clean @rowboat#0001 30` OR `!reactions clean 232921983317180416 20 :thinking:` |
| `!backups restore {user}` | Restores a user to the most recently saved member backup | Admin | `!backups restore 232921983317180416` OR `!backups restore rowboat#0001` |
| `!backups clear {user ID}` | Deletes all saved backups for a user | Admin | `!backups clear 232921983317180416` OR `!backups clear rowboat#0001` |
| `!stats {user}` | Presents general statistics for a given user | Moderator | `!stats 232921983317180416` OR `!stats rowboat#0001` |
| `!emojistats (global / server) most` | Displays the most / least used server emojis in the current guild / globally | Moderator | `!emojistats global most` OR `!emojistats server least` |
| `!voice log {user}` | Displays a list of a given user's recent voice channel activity | Moderator | `!voice log 232921983317180416` OR `!voice log @rowboat#0001` |
| `!invites prune [uses]` | Deletes server invites with the given number of uses or less. Cleans 1 and 0 use invites if left blank | Administrator | `!invites prune 5` |
| `!tracking` | Display roles tracked with members and name | Mod | `!tracking` |
| `!roleinfo {role}` | Display information about desired role | Mod | `!roleinfo  274266640403791873` |
| `!say user {user} {message}` | Send a message from the bot to the user | Administrator | `!say user @blahuser Stop being silly please` |
| `!say channel {channel} {message}` | Send a message from the bot to the specified channel | Administrator | `!say channel #rewardblah Prepare for the most amazing thing ever` |
| `!slowmode / slowmo / slownova {duration} [reason]` | Sets slowmode in the current channel for the {duration}. The duration must be between 0 and 120. Setting the duration to 0 will remove the slowmode in the channel | Mod | `!slowmode 10 People are speaking over each other` |
| `!override [duration] [inguild]` | Enable global admin override for duration. Providing `Any` will allow global admin to override and use commands in any guild. | Global Admin | `!override 30 in any` OR `!override 30 in all` OR `!override 30 in 77176186148499456` |
| `!cease` `[guild]` | Remove send message perms for the channel, or guild  everyone role if `guild` is specified | Mod | `!cease` OR `!cease guild` |
| `!uncease` `[guild]` | Restore send message perms to default value for the channel, or enable for the guild everyone role if `guild` is specified | Mod | `!uncease` OR `!uncease guild` |
| `!shut` | If called while in a voice chat, restricts the speak and use voice activation perms. \(Due to a discord bug, this does not immediately mute everyone, but forces everyone to Push-to-Talk\) | Mod | `!shut` |
| `!unshut` | Removes restrictions on speak and voice activation detection for the `@everyone` role. Must be in the voice channel. | Mod | `!unshut` |
| `!minfo {user}` | Mobile Mod trigger on user | Mod | `!minfo 76685590585671680` |
|  🔗reaction | Mobile Mod trigger on user | Mod | React to message with 🔗 | |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| role\_aliases | Aliases which can be used in place of role IDs in commands | dict | empty |
| group\_roles | Roles which can be joined and left by any user. These roles cannot grant any elevated permissions | dict | empty |
| group\_confirm\_reactions | Confirm group joins by users | bool | false |
| locked\_roles | Prevents permission changes from being made to listed roles | list | empty |
| persist | Controls the member persistence settings | dict | empty |
| tracking | roles to track in the `tracking` command to check membership | list | empty |
| allow\_say | Whether or not to enable the `say` command | bool | False |
| confirm\_actions | Confirm when actions are performed | bool | True |
| mobile\_mod\_channel | Channel to direct mobile modding dialog to go to | snowflake | None |
| onjoin\_roles | List of roles to automatically apply on a user joining | list | empty |
| welcomes | Allows configuration of guild welcomes when a member joins the server | dict | empty |

### Member Persistence Settings

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| roles | Whether to recover roles when a user rejoins the server | bool | false |
| role\_ids | A list of role ids which will be recovered if `roles` is true. Any other roles will be ignored when a user rejoins the server | list | empty |
| nickname | Whether to recover the nickname when a user rejoins the server | bool | false |
| voice | Whether to recover mute/deafen settings when a user rejoins the server | bool | false |

### Welcome Settings

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| msg | Content of the message that will be sent when a member joins the guild | unicode | None |
| dm | If the message should be a dm or not | bool | False |

### Message Tokens

| Token | Description |
| :--- | :--- |
| {user} | Will mention the user |
| {server} | Will include the server name |
| {channel} | Will link the current channel |
| {c&lt;snowflake&gt;} | Will link the specified channel |

## Configuration Example

```yaml
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

