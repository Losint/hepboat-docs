# Spam Plugin

Plugin name: `spam`

The spam plugin allows administrators and moderators to limit spam and enforce punishments on spammers. The plugin can be used to limit mass sending of:

* General Spam
* Mentions
* Links
* Attachments
* Emojis
* Newlines
* Duplicate Messages
* Upper case letters

This plugin should be enabled in conjunction with the [infractions plugin](infractions.md) for punishment implementation.

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| roles | A mapping of roles to spam configurations. | dict | empty |
| levels | A mapping of levels to spam configurations. This will match any user with a level that is equal or below. | dict | empty |

### Spam Configuration

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| max\_messages | Max `count` of messages that can be sent in `interval`. Requires a check subconfiguration. | dict | empty |
| max\_mentions | Max `count` of user mentions that can be sent in `interval`. Requires a check subconfiguration.| dict | empty |
| max\_links | Max `count` of links that can be sent in `interval`. Requires a check subconfiguration.| dict | empty |
| max_upper_case | Max `count` of upper case letters (does not have to be consecutive) that can be sent in `interval`. Requires a check subconfiguration.| dict | empty |
| max\_emojis | Max `count` of emojis that can be sent in `interval`. Requires a check subconfiguration.| dict | empty |
| max\_newlines | Max `count` of new lines/line breaks that can be sent in `interval. Requires a check subconfiguration.| dict | empty |
| max\_attachments | Max `count` of attachments that can be sent in `interval`. Requires a check subconfiguration.| dict | empty |
| max\_duplicates | Max `count` of duplicate messages that can be sent in `interval`. Requires a check subconfiguration. | dict | empty |
| punishment | Sets a punishment when spam detection is triggered. Options: `NONE, MUTE, TEMPMUTE, BAN, TEMPBAN, KICK` | str | `NONE` |
| punishment_duration | Required for `TEMPBAN` and `TEMPMUTE` punishments. Seconds that a punishment should last. | int | 300 |
| channel_whitelist | List of whitelisted channels that will not trigger spam detection for the action. | list(snowflake) | [] |
| clean | Whether or not messages that triggered the spam filter should be deleted. | bool | false |
| clean_count | Maximum number of messages to be deleted. | int | 100 |
| clean_duration | Duration in seconds in which messages should be deleted. | int | 900 |

NOTE: The [censor plugin](censor.md) also has an `all_caps` filter similar to the `max_upper_case` spam filter that is more configurable.

### Check Subconfiguration
| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| count | Number of times an action is performed in `interval` to trigger the punishment. | int | N/A |
| interval | Seconds within which a user with over `count` actions will trigger a punishment. | int | N/A |
| punishment | Sets a punishment when spam detection is triggered. Options: `NONE, MUTE, TEMPMUTE, BAN, TEMPBAN, KICK` | str | `NONE` |
| punishment_duration | Required for `TEMPBAN` and `TEMPMUTE` punishments. Seconds that a punishment should last. | int | 300 |
| channel_whitelist | List of whitelisted channels that will not trigger spam detection for the action. | list(snowflake) | [] |

## Configuration Example

```yaml
plugins:
  spam:
    levels:
      49:
        punishment: TEMPMUTE
        punishment_duration: 120
        clean: true
        clean_count: 50
        clean_duration: 500
        channel_whitelist: [390107999022350336]
        max_newlines:
          count: 60
          interval: 120
          channel_whitelist: [439205512425504771]
        max_duplicates:
          count: 5
          interval: 30
          channel_whitelist: [439205512425504771]
    roles:
      580569967364407316:
        punishment: NONE
        punishment_duration: 10
        clean: true
        max_mentions:
          count: 3
          interval: 30
  infractions:
    mute_role: 579398816072073246
```

