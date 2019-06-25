# Infractions Plugin

Plugin name: `infractions`

The infractions plugin provides a set of useful moderator commands. These commands should be used together with the configuration to help handle and track misbehaving users over time.

## Commands

Arguments in `{}` are required. Arguments in `[]` are optional.

### Moderation commands

#### Punishments
| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!warn {user} [reason]` | Adds a warning infraction to a user. | Moderator | `!warn 520047158104424488 1st warning, spamming emoji` OR `!warn @HepBoat#0361 2nd warning, going off-topic` |
| `!kick {user} [reason]` | Kicks a user from the server. | Moderator | `!kick 520047158104424488 spamming` OR `!kick @HepBoat#0361 spamming` |
| `!mkick {users} -r [reason]` | Kicks multiple users from the server. | Moderator | `!mkick 232921983317180416 80351110224678912 108598213681922048 -r spamming` |
| `!ban {user} [reason]` | Bans a user from the server. | Moderator | `!ban 520047158104424488 spamming` OR `!ban @HepBoat#0361 spamming` |
| `!mban {users] -r [reason]` | Bans multiple users from the server | Moderator | `!mban 232921983317180416 80351110224678912 108598213681922048 -r spamming` |
| `!unban {user} [reason]` | Unbans a user from the server. | Moderator | `!unban 520047158104424488` |
| `!softban {user} [reason]` | Softbans (bans/unbans) a user and deletes any of their messages that were sent within the last 7 days. | Moderator | `!softban 520047158104424488 spamming` OR `!softban @HepBoat#0361 spamming` |
| `!tempban {user} {duration} [reason]` | Temporarily bans a user. | Moderator | `!tempban 520047158104424488 5h spamming` OR `!tempban @HepBoat#0361 5h spamming` |
| `!munban {users} -r [reason]` | Unbans multiple users from the server. | Moderator | `!munban 232921983317180416 80351110224678912 108598213681922048 -r spamming` |

#### Mutes
| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!mute {user} [reason]` | Mutes a user. `mute_role` must be set in the config. | Moderator | `!mute 520047158104424488 spamming` OR  `!tempmute @HepBoat#0361 60m spamming` |
| `!mmute {users} -r [reason]` | Mutes multiple users on the server. | Moderator | `!mmute 232921983317180416 80351110224678912 108598213681922048 -r spamming` |
| `!unmute {user}` | Unmutes a user | Moderator | `!unmute 520047158104424488` |
| `!munmute {users} -r [reason]` | Unmute multiple users on the server. | Moderator | `!munmute 232921983317180416 80351110224678912 108598213681922048 -r spamming` |
| `!tempmute {user} {duration} [reason]` | Temporarily mutes a user. `mute_role` must be set in the config. | Moderator | `!tempmute 520047158104424488 30m spamming` OR `!tempmute @HepBoat#0361 30m spamming` |
| `!hardmute enable {user} [reason]` | Hard-mutes a user. `hard_mute_role` must be set in the config. | Moderator | `!hardmute enable @user1 being really silly` |
| `!hardmute temp {user} {duration} [reason]` | Hard-mutes a user temporarily. `hard_mute_role` must be set in the config. | Moderator | `!hardmute temp @user1 6h being really silly` |
| `!hardmute disable {user}` | Disables an active hard-mute on a user. | Moderator | `!hardmute disable @user1` |

A regular `mute` will apply the `mute_role` to a user. A `hardmute` will apply the `hard_mute_role` to the user AND remove all other roles from the user except the ones configured in `hard_mute_ignore`.

Disabling a regular `mute` will remove the `mute_role` from the user. Disabling a `hard_mute_role` will remove the `hard_mute_role` AND restore all original roles before the hard-mute back to the user.

#### User
| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!report [reason]` | Send a report to a report channel. `report_channel` must be configured. | Default | `!report @Tobiah is being a meanie` |
| `!timeleft` | Allow a muted user to check their remaining time in their mute. | Default | `!timeleft` |
| `!selfmute {duration}` OR `!muteself {duration}` | Self mutes for the given duration. `selfmute` and `mute_role` must be enabled in the config. | Default | `!selfmute 2m` |

### Miscellaneous commands

| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!inf archive` | Creates a CSV file of all infractions on the server. | Administrator | `!infractions archive` |
| `!inf search {query}` | Searches infractions database for given query. | Moderator | `!inf search 520047158104424488` OR `!inf search HepBoat#0361` OR `!inf search spamming` |
| `!inf info {inf#}` | Presents information on the given infraction. | Moderator | `!inf info 1274` |
| `!inf delete {inf#}` | Delete infraction. | Administrator | `!inf delete 1274` |
| `!inf cleanall {user}` | Clean out all infractions (excluding notes) for the given user in the guild. | Moderator | `!inf cleanall 520047158104424488` |
| `!inf duration {inf#} {duration}` | Updates the duration of the given infraction. Duration starts from time of initial action. | Moderator | `!inf duration 1274 5h` |
| `!inf reason {inf#} {reason}` | Updates the reason of a given infraction. | Moderator | `!inf reason 1274 rude behaviour towards staff` |
| `!inf recent [num]` | Get recent `num` infractions. Default `num` is 10. | Moderator | `!inf recent 5` |
| `!inf active [num]` | Get recent `num` active infractions. Default `num` is 10. | Moderator | `!inf active 5` |
| `!inf mutes [num]` | Get recent `num` mutes. Default `num` is 10. | Moderator | `!inf mutes 5` |
| `!inf bans [num]` | Get recent `num` bans. Default `num` is 10. | Moderator | `!inf bans 5` |
| `!note add {user} [reason]` | Add a note on a user. | Moderator | `!note add 222617379421683712 omaiwamo shinderu` |
| `!note delete {inf#}` | Delete note on user. | Administrator | `!note delete 1275` |
| `!note info {inf#}` | Get full details on a note. | Moderator | `!note info 1275` |
| `!note search {query}` | Search for a note with the specified query. | Moderator | `!note search @user1` |
| `!note archive` | Creates a CSV file of all notes on the server. | Administrator | `!note archive` |
| `!temprole {user} {role} {duration} [reason]` | Adds a role temporarily to a user. Will be logged as an note. | Moderator | `!temprole @user1 StronkRole 1h stronk for 1h` |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| confirm\_actions | Whether to confirm actions with a message reply. | bool | true |
| confirm\_actions\_reaction | Whether to confirm actions with a checkmark reaction on the command. | bool | false |
| confirm\_actions\_expiry | Seconds after which to delete the confirmed action message. If zero the message will never be deleted. | int | 0 |
| mute\_role | Role ID added for muted users. | snowflake | empty |
| hard\_mute\_role | Role ID added for hard-muted users. | snowflake | empty |
| hard\_mute\_ignore | List of role IDs that will not be removed upon a hard-mute. | list(snowflake) | empty |
| reason\_edit\_level | Minimum level for users to edit infraction reasons made by other users. | int | 100 |
| duration\_edit\_level | Minimum level for users to edit infraction durations made by other users. | int | 100 |
| report\_channel | Channel ID for report collection. | snowflake | empty |
| report\_role | Role ID to ping for reports. | snowflake | empty |
| vc\_mute | Whether or not to attempt to move a muted voice user to a guild-defined AFK channel. | bool | false |
| vc\_mute\_channel | Override channel ID for guild-defined AFK channel. | snowflake | empty |
| selfmute | Whether to allow selfmutes. | bool | false |
| selfmute_max | Maximum seconds for a selfmute duration.  | int | 1209600 (2 weeks) |
| selfmute\_role | Role ID assigned to self-mute users. | snowflake | empty |
| notify | Dictionary of infraction types to notify configurations. | dict | empty |

### Notify Configuration Options

Valid actions: `WARN`, `TEMPMUTE`, `MUTE`, `TEMPMUTEHARD`, `MUTEHARD`, `TEMPBAN`, `BAN`

NOTE: The [`modlog` plugin](modlog.md) needs to be enabled for notifications to work properly.

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| format | Format for infraction DM notifications. If `true` is specified, it will use the default notify configuration. | str | None |
| emoji | Emoji to override for the config | str | no\_mouth |

## Configuration Example

```yaml
plugin:
  infractions:
    confirm_actions: false
    mute_role: 289494296703533058
    reason_edit_level: 50
    report_channel: 297917022300274688
    vc_mute: true
    vc_mute_channel: 77177426521624576
    notify:
      WARN:
        format: true
      TEMPMUTE:
        format: true
      TEMPBAN:
        format: true
      KICK:  
        format: true
```

## Custom Infractions Format

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">{action!s}</td>
      <td style="text-align:left">
        <p>infraction action</p>
      </td>
    </tr>  
    <tr>
      <td style="text-align:left">{guild.name}</td>
      <td style="text-align:left">
        <p>guild name</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">{actor!s} </td>
      <td style="text-align:left">
        <p>command author (username#discriminator)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">{reason!s}</td>
      <td style="text-align:left">
        <p>infraction reason</p>
      </td>
    </tr> 
    <tr>
      <td style="text-align:left">{expires} </td>
      <td style="text-align:left">
        <p>expiration date</p>
      </td>
    </tr>
  </tbody>
</table>

### Custom Format Configuration Example

```yaml
plugin:
  infractions:
    notify:
      WARN:
        emoji: warning
        format: |-
          You have been **{action!s}** in **{guild.name}** by **{actor!s}** for `{reason!s}`.
      TEMPMUTE:
        emoji: no_mouth
        format: |-
          You have been **{action!s}** in **{guild.name}** by **{actor!s}** for `{reason!s}` until **{expires}** GMT+0.
      MUTE:
        emoji: no_mouth
        format: |-
          You have been **{action!s}** in **{guild.name}** by **{actor!s}** for `{reason!s}`.
      TEMPBAN:
        emoji: tools
        format: |-
          You have been **{action!s}** until **{expires} GMT+0 in **{guild.name}** by **{actor!s}** for `{reason!s}`.
      BAN:
        emoji: tools
        format: |-
          You have been **{action!s}** in **{guild.name}** by **{actor!s}** for `{reason!s}`
      KICK:
        emoji: boot
        format: |-
          You have been **{action!s}** in **{guild.name}** by **{actor!s}** for `{reason!s}`.
          ```