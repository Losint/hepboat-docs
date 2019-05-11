# ModLog Plugin

The modlog plugin provides a mechanisim for logging various events and actions to one or more channels. The intention of the modlog is to provide a private feed of server events that administrators and moderators can use to better monitor and audit users actions. The modlog is extremely configurable, and thus fairly complex.

## Commands

| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!modlog hush` | Disables tracking of message deletes in modlog | Administrator | `!modlog hush` |
| `!modlog unhush` | Re-enables tracking of message deletes | Administrator | `!modlog unhush` |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| ignored\_users | A list of user ids which are ignored in the modlog. This is useful for ignoring bots that regularly delete or edit their messages | list | empty |
| ignored\_channels | A list of channel ids which are ignored in the modlog. This is useful for ignoring private or high-activity channels | list | empty |
| new\_member\_threshold | The number of seconds an account is considered new | int | 900 \(15 minutes\) |
| channels | Mapping of channel names/ids to ModLog Configurations | dict | empty |

### ModLog Configuration

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| include | List of modlog actions to include. If empty this includes all mod log actions | list | empty |
| exclude | List of modlog actions to exclude. If empty this excludes no mod log actions | list | empty |
| timestamps | Whether to render timestamps along with loglines | bool | false |
| timezone | The timezone that timestamps are rendered in. [Supported timezones](https://gist.github.com/heyalexej/8bf688fd67d7199be4a1682b3eec7568) | timezone | US/Eastern |
| custom | Change the logging format if the `CUSTOM` flag is on for the guild | dict | empty |

## Actions

| Action | Description |
| :--- | :--- |
| CHANNEL\_CREATE | A channel is created |
| CHANNEL\_DELETE | A channel is deleted |
| GUILD\_MEMBER\_ADD | A member joins |
| GUILD\_MEMBER\_REMOVE | A member leaves \(or gets kicked\) |
| GUILD\_ROLE\_CREATE | A role is created |
| GUILD\_ROLE\_DELETE | A role is deleted |
| GUILD\_BAN\_ADD | A ban is added |
| MEMBER\_ROLE\_ADD | A role is added to a member |
| MEMBER\_ROLE\_RMV | A role is removed from a member |
| MEMBER\_TEMP\_MUTED | A tempmute is added |
| MEMBER\_MUTED | A mute is added |
| MEMBER\_UNMUTED | A mute is removed |
| MEMBER\_KICK | A member is kicked |
| MEMBER\_BAN | A ban \(with a reason\) is added |
| MEMBER\_SOFTBAN | A softban is added |
| MEMBER\_TEMPBAN | A tempban is added |
| MEMBER\_WARNED | A warning is added |
| MEMBER\_RESTORE | A user rejoined and had their roles/nickname/etc restored |
| ADD\_NICK | A user adds a nickname |
| RMV\_NICK | A user removes a nickname |
| CHANGE\_NICK | A user changes their nickname |
| CHANGE\_USERNAME | A user changes their username |
| MESSAGE\_EDIT | A message is edited |
| MESSAGE\_DELETE | A message is deleted |
| MESSAGE\_DELETE\_BULK | Multiple messages are deleted |
| VOICE\_CHANNEL\_JOIN | A user joins a voice channel |
| VOICE\_CHANNEL\_LEAVE | A user leaves a voice channel |
| VOICE\_CHANNEL\_MOVE | A user moves voice channels |
| COMMAND\_USED | A user uses a rowboat command |
| SPAM\_DEBUG | A user triggered spam protection |
| CENSORED | A user posted a message that was censored by the bot |
|  ADD\_NOTE | A note added on a user |
| SLOWMODE\_ON | Slowmode is enabled \(or altered\) in a channel |
| SLOWMODE\_OFF | Slowmode is disabled in a channel |

## Configuration Example

```text
  modlog:
    channels:
      289494042000228352:
        timestamps: true
        timezone: Etc/GMT-8
        exclude: []
        include: []
    ignored_users: [84912325282254848]
    new_member_threshold: 86400
    custom:
      MEMBER_WARNED:
        emoji: warning
        format: |-
          WARNING
          **User**: {member!s} | <@{member.id}>
          **Moderator**: {actor!s}
          **ID**: {member.id}
          **Reason**: {reason!s}
```

## Custom Mod Log Format

After you have run the `@HepBoat#0361 setup` command you will need to contact a Global Administrator to get the custom formats enabled in your guild. You may then follow the configuration bellow to fully customize the modlog to your liking.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">{e.author!s}</td>
      <td style="text-align:left">
        <p>username#discriminator</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">{e.author.id}</td>
      <td style="text-align:left">
        <p>user id</p>
      </td>
    </tr> 
    <tr>
      <td style="text-align:left">{e.channel.mention}</td>
      <td style="text-align:left">
        <p>channel mention</p>
      </td>
    </tr> 
    <tr>
      <td style="text-align:left">{e.channel}</td>
      <td style="text-align:left">
        <p>channel name</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">{e.user!s}</td>
      <td style="text-align:left">
        <p>username#discriminator if they leave</p>
      </td>
    </tr> 
    <tr>
      <td style="text-align:left">{e.user.id} </td>
      <td style="text-align:left">
        <p>user id if they leave</p>
      </td>
    </tr>  
    <tr>
      <td style="text-align:left">{actor!s} </td>
      <td style="text-align:left">
        <p>command author</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">{reason!s}</td>
      <td style="text-align:left">
        <p>infraction reason</p>
      </td>
    </tr> 
      <td style="text-align:left">{expires} </td>
      <td style="text-align:left">
        <p>expiration date</p>     
  </tbody>
</table>

## Example Custom Mod Log Configuration

```text
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
          **ID**: {e.user.id}'
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
          **{author!s}'s** (**ID:** {author.id}) messages was deleted in **{e.channel.mention}** ({e.channel}):
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
