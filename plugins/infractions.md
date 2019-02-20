# Infractions Plugin

The infractions plugin provides a set of useful moderator commands. These commands are intended to be used together and help handle/track misbehaving users over time.

## Commands

| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!warn {user} [reason]` | Adds a warning infraction to a user | Moderator | `!warn 232921983317180416 1st warning, spamming emoji` OR `!warn @rowboat#0001 2nd warning, going off-topic` |
| `!mute {user} [reason]` | Mutes a user. This will only work if `mute_role` is set in the config | Moderator | `!mute 232921983317180416 spamming` OR  `!tempmute @rowboat#0001 60m spamming` |
| `!unmute {user}` | Unmutes a user | Moderator | `!unmute 232921983317180416` |
| `!tempmute {user} {duration} [reason]` | Temporarily mutes a user. Will only work if `temp_mute_role` or `mute_role` is set in the config | Moderator | `!tempmute 232921983317180416 30m spamming` OR `!tempmute @rowboat#0001 30m spamming` |
| `!kick {user} [reason]` | Kicks the user from the server | Moderator | `!kick 232921983317180416 spamming` OR `!kick @rowboat#0001 spamming` |
| `!mkick {users] -r [reason]` | Kicks multiple users from the server | Moderator | `!mkick 232921983317180416 80351110224678912 108598213681922048 -r spamming` |
| `!ban {user} [reason]` | Bans a user from the server | Moderator | `!ban 232921983317180416 spamming` OR `!ban @rowboat#0001 spamming` |
| `!unban {user} [reason]` | Unbans a user | Moderator | `!unban 232921983317180416` |
| `!softban {user} [reason]` | Softbans \(bans/unbans\) a user and deletes the user's messages sent within the last 7 days | Moderator | `!softban 232921983317180416 spamming` OR `!softban @rowboat#0001 spamming` |
| `!tempban {user} {duration} [reason]` | Temporarily bans a user | Moderator | `!tempban 232921983317180416 5h spamming` OR `!tempban @rowboat#0001 5h spamming` |
| `!inf archive` | Creates a CSV file of all infractions on the server | Administrator | `!infractions archive` |
| `!inf search {query}` | Searches infractions database for given query | Moderator | `!inf search 232921983317180416` OR `!inf search rowboat#0001` OR `!inf search spamming` |
| `!inf info {inf#}` | Presents information on the given infraction | Moderator | `!inf info 1274` |
| `!inf delete {inf#}` | Delete infraction | Admin | `!inf delete 1274` |
| `!inf duration {inf#} {duration}` | Updates the duration of the given infraction. Duration starts from time of initial action | Moderator | `!inf duration 1274 5h` |
| `!inf reason {inf#} {reason}` | Updates the reason of a given infraction | Moderator | `!inf reason 1274 rude behaviour towards staff` |
| `!slowmo {time in seconds}` | Sets the slowmode time for the channel | Moderator | `!slowmo 10` |
| `!slowmo 0` | Turn off slowmode for the channel | Moderator | `!slowmo 0` |
| `!report {message}` | Send a report to a report channel | Everyone | `!report @Tobiah is being a meanie` |
| `!selfmute / muteself {duration}` | Mute yourself for the given duration. Maximum of `2w` | Everyone | `!selfmute 2m` |
| `!note add {user} {note}` | Add a note on a user | Mod | `!note add 222617379421683712 omaiwamo shinderu` |
| `!note delete {inf#}` | Delete note on user | Admin | `!note delete 1275` |
| `!note info {inf#}` | Get full details on a note | Mod | `!note info 1275` |
| `!note search {query}` | Search for a note with the specified query | Mod | `!note search @user1` |
| `!inf recent {# recent}` | Get recent infractions | Mod | `!inf recent 5` |
| `!note archive` | Get an archive of notes | Admin | `!note archive` |
| `!temprole {user} {role} {duration} {reason}` | Adds a role temporarily to a user | Mod | `!temprole @user1 StronkRole 1h stronk for 1h` |
| `!hardmute enable {user} {reason}` | Hard mutes a user | Mod | `!hardmute enable @user1 being really silly` |
| `!hardmute temp {user} {duration} {reason}` | Hard mutes a user temporarily | Mod | `!hardmute temp @user1 6h being really silly` |
| `!hardmute disable {user}` | Disables an active hard mute on a user | Mod | `!hardmute disable @user1` |
| `!mban {users] -r [reason]` | Bans multiple users from the server | Moderator | `!mban 232921983317180416 80351110224678912 108598213681922048 -r spamming` |
| `!munban {users] -r [reason]` | Unbans multiple users from the server | Moderator | `!munban 232921983317180416 80351110224678912 108598213681922048 -r spamming` |
| `!mmute {users] -r [reason]` | Mutes multiple users on the server | Moderator | `!mmute 232921983317180416 80351110224678912 108598213681922048 -r spamming` |
| `!munmute {users] -r [reason]` | Unmute multiple users on the server | Moderator | `!munmute 232921983317180416 80351110224678912 108598213681922048 -r spamming` |
| `!timeleft` | Allow muted user to check their remaining time in their mute | Default | `!timeleft` |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| confirm\_actions | Whether to confirm that an action was done in the current channel | bool | true |
| confirm\_actions\_reaction | Whether to confirm actions done in the channel using a checkmark reaction | bool | false |
| confirm\_actions\_expiry | The duration after which to delete the confirmed action message. If zero the message will never be deleted | int | 0 |
| mute\_role | Role ID that is set for users who are muted | id | none |
| reason\_edit\_level | Minimum level to allow users to edit other users' infraction reasons | int | 100 |
| report\_channel | Channel to send reports to | id | none |
| report\_role | Role to ping for reports | id | none |
| selfmute | Whether to allow selfmutes | bool | false |
| selfmute\_max | Maximum duration for a selfmute in seconds.  | int | 1209600 \(2 weeks\) |
| selfmute\_role | Role ID that is set for users who self-mute | id | none |
| notify | Configure what infractions should notify users | dict | none |
| hard\_mute\_role | Role ID that is set for users who are hard-muted | id | none |
| hard\_mute\_ignore | Users belonging to any of the defined role id's will ignore any hard mutes | list id | \[\] |
| vc\_mute | Whether or not to attempt to move muted user to guild defined AFK channel | bool | false |
| vc\_mute\_channel | Channel to override guild define AFK channel with. Requires `vc_mute` | id | none |

## Notify Sub-configuration

Valid Actions: `WARN`, `TEMPMUTE`, `MUTE`, `TEMPBAN`, `BAN`

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| format | Format for warn notifications. if "true" is specified, it will use the default configuration | string | false |
| emoji | Emoji to override for the config | string | no\_mouth |

## Configuration Example

```yaml
  infractions:
    confirm_actions: false
    mute_role: 289494296703533058
    reason_edit_level: 50
    report_channel: 297917022300274688
    vc_mute: true
    vc_mute_channel: 77177426521624576
    notify:
      WARN:
        format: |-
          {action!s}
          You have been **{action!s}**
          **Guild**: {guild.name}
          **Moderator**: {actor!s}
          **Reason**: {reason!s}
      TEMPMUTE:
        format: |-
          {action!s}
          You have been **{action!s}**
          **Guild**: {guild.name}
          **Moderator**: {actor!s}
          **Expires**: {expires} GMT+0
          **Reason**: {reason!s}
      MUTE:
        format: false
      TEMPBAN:
        format: |-
          {action!s}
          You have been **{action!s}**
          **Guild**: {guild.name}
          **Moderator**: {actor!s}
          **Expires**: {expires} GMT+0
          **Reason**: {reason!s}
      BAN:
        format: true
```