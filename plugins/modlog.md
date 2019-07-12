# ModLog Plugin

Plugin name: `modlog`

The modlog plugin provides a mechanism for logging various events and actions to one or more channels. The intention
 of the modlog is to provide a private feed of server events that administrators and moderators can use to better 
 monitor and audit users actions. The modlog is extremely configurable and thus fairly complex.

## Commands

| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!modlog hush` | Disables tracking of message deletes in modlog. | Administrator | `!modlog hush` |
| `!modlog unhush` | Re-enables tracking of message deletes. | Administrator | `!modlog unhush` |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| ignored\_users | A list of user IDs which are ignored in the modlog. This is useful for ignoring bots that regularly delete or edit their messages | list(snowflake) | empty |
| ignored\_channels | A list of channel IDs which are ignored in the modlog. This is useful for ignoring private or high-activity channels | list(snowflake) | empty |
| new\_member\_threshold | The number of seconds an account is considered new. | int | 900 \(15 minutes\) |
| channels | Mapping of channel names or ids to ModLog configurations | dict | empty |
| custom | Change the logging format if the `CUSTOM` flag is on for the guild. Only available for PLAIN mode logs. | dict | empty | 

### ModLog Configuration

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| include | List of modlog actions to include. If empty this includes all mod log actions. | list | empty |
| exclude | List of modlog actions to exclude. If empty this excludes no mod log actions. | list | empty |
| mode | Type of log output. Options: PLAIN, PRETTY. Pretty mode uses embedded messages. | str | PLAIN | 
| exclude_category | A list of category IDs which are ignored in the modlog. | list(snowflake) | empty | 
| timestamps | Show timestamps with the logs in PLAIN mode. | bool | false |
| timezone | The timezone that timestamps are rendered in in PLAIN mode. [Supported timezones.](https://gist.github.com/heyalexej/8bf688fd67d7199be4a1682b3eec7568) | timezone | US/Eastern |

NOTE: If an action is in both include and exclude lists, the action will be excluded.

## Actions

### Server actions
| Action | Description |
| :--- | :--- |
| CHANNEL\_CREATE | A channel is created |
| CHANNEL\_DELETE | A channel is deleted |
| CATEGORY\_CREATE | A category is created | 
| CATEGORY\_DELETE | A category is deleted |
| GUILD\_MEMBER\_ADD | A member joins |
| GUILD\_MEMBER\_REMOVE | A member leaves |
| GUILD\_ROLE\_CREATE | A role is created |
| GUILD\_ROLE\_DELETE | A role is deleted |
| SLOWMODE\_ON | Slowmode is enabled or altered in a channel |
| SLOWMODE\_OFF | Slowmode is disabled in a channel |
| BOT_DEBUG | A command failed |

### User actions
| Action | Description |
| :--- | :--- |
| COMMAND\_USED | A user uses a HepBoat command |
| ADD\_NICK | A user adds a nickname |
| CHANGE\_NICK | A user changes their nickname |
| CHANGE\_USERNAME | A user changes their username |
| RMV\_NICK | A user removes a nickname |
| GUILD_MEMBER_ROLES_ADD | A role is added to a user |
| GUILD_MEMBER_ROLES_RMV | A role is removed from a user |
| MEMBER\_RESTORE | A user rejoined and had their roles/nickname/etc restored |
| MEMBER\_ROLE\_ADD | A role is added to a user by command |
| MEMBER_ROLE_REMOVE | A role is removed from a user by command |
| VOICE\_CHANNEL\_JOIN | A user joins a voice channel |
| VOICE\_CHANNEL\_LEAVE | A user leaves a voice channel |
| VOICE\_CHANNEL\_MOVE | A user moves voice channels |

### Message actions
| Action | Description |
| :--- | :--- |
| MESSAGE\_EDIT | A message is edited |
| MESSAGE\_DELETE | A message is deleted |
| MESSAGE\_DELETE\_BULK | Multiple messages are deleted |

### Spam actions
| Action | Description |
| :--- | :--- |
| CENSOR_DEBUG | A user triggered too many censor violations |
| CENSORED | A user posted a message that was censored by the bot |
| CHANGE_NICK_BLOCKED | A nick change is blocked |
| SPAM\_DEBUG | A user triggered spam protection |

### Infraction actions
| Action | Description |
| :--- | :--- |
| MEMBER\_MUTED | A mute is added for a user|
| MEMBER\_UNMUTED | A mute is removed for a user |
| MEMBER\_HARD\_MUTED | A hard mute is added for a user |
| MEMBER\_HARD\_UNMUTED | A hard mute is removed for a user |
| MEMBER\_HARD\_TEMP_MUTED | A hard temp-mute is added for a user |
| MEMBER\_TEMP\_MUTED | A temp-mute is added for a user |
| MEMBER_TEMPMUTE_EXPIRE | A temp-mute expired for a user |
| MEMBER\_KICK | A member is kicked for a user |
| MEMBER\_BAN | A ban \(with a reason\) is added for a user |
| MEMBER\_SOFTBAN | A softban is added for a user |
| MEMBER\_CLEANBAN | A cleanban is added for a user |
| MEMBER\_TEMPBAN | A tempban is added for a user |
| MEMBER_TEMPBAN_EXPIRE | A tempban expired for a user |
| MEMBER\_WARNED | A warning is added for a user |
| ADD\_NOTE | A note added on a user |
| GUILD\_BAN\_ADD | A ban is added to the guild |
| GUILD_BAN_REMOVE | A ban is removed from the guild|
| RAID | Potential raid detected |
| RAID_MEMBER | Raid role applied to user |

## Configuration Example

```yaml
plugins:
  modlog:
    channels:      
      289494042000228352:
        mode: pretty
        include: []
        exclude: [MESSAGE_EDIT]
    ignored_users: [84912325282254848]
    new_member_threshold: 86400
```

## Custom Mod Log Format

After you have run the `@HepBoat#0361 setup` command you will need to contact a Global Administrator to enable custom formats for PLAIN mode modlogs in your guild. You may then follow the configuration below to fully customize the modlog to your liking.

| Option | Description |
| :--- | :--- |
| `{e.author!s}`	| username#discriminator |
| `{e.author.id}` | user id |
| `{e.channel.mention}` | channel mention |
| `{e.channel}` | channel name |
| `{e.user!s}` | username#discriminator if they leave |
| `{e.user.id}` | user id if they leave |
| `{actor!s}` | command author |
| `{reason!s}` | infraction reason |
| `{expires}` | expiration date |

NOTE: If configured improperly, your logs may be missing and lost. Customize at your own risk.

### Configuration Example

```yaml
plugins:
  modlog:
    custom:
      CENSORED:
        emoji: no_entry_sign
        format: |-
          **{e.author!s}**'s message (**ID**: {e.author.id}) censored in channel **{e.channel.mention}** ({e.channel}):
          {c.details}:
          ```
          {c.content!s}
          ```
      GUILD_BAN_ADD:
        emoji: hammer
        format: |-
          BAN
          **User**: {e.user!s}
          **ID**: {e.user.id}
          **Reason**: {reason!s}
      GUILD_MEMBER_ADD:
        emoji: wave
        format: |-
          **{e.user!s}** (**ID**: {e.user.id}) (<@{e.user.id}>) has joined the server. Say hi or ban! {new} (created {created})
      GUILD_MEMBER_REMOVE:
        emoji: outbox_tray
        format: |-
          **{e.user!s}** has left the server
      GUILD_SOFTBAN_ADD:
        emoji: hammer
        format: |-
          SOFT-BAN
          **User**: {e.user!s}
          **Moderator**: {actor!s}
          **ID**: {e.user.id}
          **Reason**: {reason!s}
      GUILD_TEMPBAN_ADD: 
        emoji: hammer
        format: |-
          TEMPORARY BAN
          **User**: {e.user!s}
          **ID**: {e.user.id}
          **Moderator**: {actor!s}
          **Expires at**: {expires} GMT+0
          **Reason**: {reason!s}
      MEMBER_BAN:
        emoji: hammer
        format: |-
          BAN
          **User**: {user!s}
          **Moderator**: {actor!s}
          **ID**: {user_id}
          **Reason**: {reason!s}
      MEMBER_KICK:
        emoji: boot
        format: |-
          KICK
          **User**: {member!s}
          **Moderator**: {actor!s}
          **ID**: {member.id}
          **Reason**: {reason!s}
      MEMBER_MUTED: 
        emoji: no_mouth
        format: |-
          MUTE
          **User**: {member!s}
          **Moderator**: {actor!s}
          **ID**: {member.id}
          **Reason**: {reason!s}
      MEMBER_ROLE_ADD: 
        emoji: key
        format: |-
          **Role Added:** {role.name}
          **To**: {member!s}
          **By:** {actor!s}
          **ID**: {member.id}
          **Reason**: {reason!s}
      MEMBER_ROLE_REMOVE:
        emoji: key
        format: |-
          **Role Removed:** {role.name}
          **To**: {member!s}
          **By:** {actor!s}
          **ID**: {member.id}
          **Reason**: {reason!s}
      MEMBER_SOFTBAN:
        emoji: hammer
        format: |-
          SOFT-BAN
          **User**: {member!s}
          **Moderator**: {actor!s}
          **ID**: {member.id}
          **Reason**: {reason!s}
      MEMBER_TEMPBAN:
        emoji: hammer
        format: |-
          TEMPORARY BAN
          **User**: {member!s}
          **Moderator**: {actor!s}
          **ID**: {member.id}
          **Expires at**: {expires} GMT+0
          **Reason**: {reason!s}
      MEMBER_TEMPBAN_EXPIRE:
        emoji: hammer
        format: |-
          UNBAN
          **User**: {user!s}
          **ID of infraction**: {inf.id}
          **ID**: {user_id}
      MEMBER_TEMPMUTE_EXPIRE:
        emoji: open_mouth
        format: |-
          MUTE EXPIRED
          **User**: {member!s}
          **ID of infraction**: {inf.id}
          **ID**: {member.id}
      MEMBER_TEMP_MUTED:
        emoji: no_mouth
        format: |-
          TEMP MUTE
          **User**: {member!s} | <@{member.id}>
          **Moderator**: {actor!s}
          **ID**: {member.id}
          **Expires**: {expires} GMT+0
          **Reason**: {reason!s}
      MEMBER_UNMUTED:
        emoji: open_mouth
        format: |-
          UNMUTED
          **User**: {member!s}
          **Moderator**: {actor!s}
          **ID**: {member.id}
      MEMBER_WARNED:
        emoji: warning
        format: |-
          WARNING
          **User**: {member!s} | <@{member.id}>
          **Moderator**: {actor!s}
          **ID**: {member.id}
          **Reason**: {reason!s}
      MESSAGE_DELETE:
        emoji: wastebasket
        format: |-
          **{author!s}'s** (**ID:** {author.id}) messages was deleted in **{channel.mention}** ({channel}):
          ```
          {msg!s}
          ```
          {attachments}
      MESSAGE_DELETE_BULK:
        emoji: wastebasket
        format: |-
          {count} messages deleted in **{channel.mention}** ({channel})
          (<{log}>)
      MESSAGE_EDIT:
        emoji: pencil
        format: |-
          **{e.author!s}'s** (**ID:** {e.author.id}) messages was edited in **{e.channel.mention}** ({e.channel} | {e.channel.id}):
          **Before:**
          ```
          {before!s}
          ```
          **After:**
          ```
          {after!s}
          ```       
      SLOWMODE_ON:
        emoji: snail
        format: |-
          Slowmode set to {time!s}s in <#{channel.id}> by **{actor!s}**
          `{reason!s}`
      SLOWMODE_OFF:
        emoji: runner
        format: |-
          Slowmode disabled in <#{channel.id}> by **{actor!s}** ```
