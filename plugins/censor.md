# Censor Plugin

Plugin name: `censor`

The censor plugin provides administrators and moderators a simple way to filter certain types of malicious and offensive content, such as:

* Invite Links
* URLs
* Inappropriate or offensive words (attachment names included)

This plugin combined with the [spam plugin](spam.md) can result in a very robust automatic abuse-prevention system. This plugin should be enabled in conjunction with the [infractions plugin](infractions.md) for punishment implementation. 

## Commands

| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!antiraid` OR `!raid` | Show if antiraid measures are active. | Moderator | `!antiraid` |
| `!antiraid disable` OR `!raid disable` | Disable antiraid and remove the `raidrole` from all members. | Moderator | `!raid disable` |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| levels | A mapping of levels to censor configurations. This will match any user with a level that is equal or lower. | dict | empty |
| channels | A mapping of channels to censor configurations. | dict | empty |

### Censor Configuration

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| filter\_zalgo | Whether to filter zalgo text from messages. | bool | true |
| zalgo\_channel\_whitelist | Array of channels to whitelist for zalgo messages | list(snowflake) | empty |
| filter\_invites | Whether to filter invite links or vanities from messages. | bool | true |
| invites\_guild\_whitelist | A list of whitelisted guild IDs for invite codes or vanities. | list(snowflake) | empty |
| invites\_whitelist | A list of whitelisted invite codes or vanities. | list(str) | empty |
| invites\_blacklist | A list of blacklisted invite codes or vanities. | list(str) | empty |
| invites\_channel\_whitelist | Array of channels to whitelist for invites. | list(snowflake) | empty |
| filter\_domains | Whether to filter URLs in messages based on domain. (e.g. `imgur.com`)| bool | true |
| domains\_whitelist | A whitelist of domain names. | list(str) | empty |
| domains\_blacklist | A blacklist of domain names. | list(str) | empty |
| domains\_channel\_whitelist | Array of channels to whitelist for domains. | list(snowflake) | empty |
| blocked\_words | A list of words \(must be separated by a boundary\) that are blacklisted. Also includes attachment names. | list(str) | empty |
| blocked\_tokens | A list of tokens \(can appear in the middle of words\) that are blacklisted. Also includes attachment names. | list(str) | empty |
| words\_channel\_whitelist | Array of channels to whitelist for blocked words and tokens. | list(snowflake) | empty |
| blocked\_mentions | A list of blacklisted mentions. See "Blocked Mention Tokens" for setup details. | list(str) | empty | 
| mention\_channel\_whitelist | Array of channels to whitelist for blocked mentions. | list(snowflake) | empty | 
| filter_all_caps | Whether to filter messages that contain a certain number of consecutive all capital letters. Spaces in messages are ignored when counting. | bool | false |
| all_caps_min_char_length | Minimum length of consecutive all capital letters to censor. | int | 5 |
| all_caps_min_message_count  | Minimum number of violating messages in `all_caps_interval` trigger the censor. | int | 3 |
| all_caps_interval  | Seconds in which over `all_caps_min_message_count` of messages will trigger the censor. | int | 30 |
| all_caps_channel_whitelist | Array of channels to whitelist for all caps filter. | list(snowflake) | empty | 
| blocked\_nicknames | A list of names \(can appear in the middle of nicknames\) that are blacklisted | list(str) | empty |
| block\_zalgo\_nicknames | Whether to filter nicknames with zalgo text | bool | false |
| message\_char\_limit | Maximum allowed message length. If set to `0`, no limit is set. | int | 0 |
| char\_limit\_channel\_whitelist | Array of channels to whitelist for message character limit. | list(snowflake) | empty |
| warn\_on\_censor | Whether to automatically DM a user when their name or message is censored. | bool | false |
| mute\_violations | Enable ability to mute a user after a set number of violations.  | bool | false |
| mute\_violations\_count | Number of violations that can be accrued in `mute_violations_interval` before muting. | int | 3 |
| mute\_violations\_interval | Seconds within which a user with over `mute_violations_count` violations will trigger a mute. | int | 10 |
| mute\_violations\_duration | Seconds to mute a user with sufficient violations. | int | 300 |
| antiraid | A single antiraid configuration. | dict | None |

When available, only whitelists or only blacklists will be checked. Whitelists will be checked first if both are configured.

A user will accrue one violation for each message that triggers a censor deletion.

### Blocked Mention Tokens
| Token | Description | Example |
| :--- | :--- | :--- |
| {r&lt;snowflake&gt;} | Will censor mentions of the specified role. | `r579304983896391680` |
| {c&lt;snowflake&gt;} | Will censor mentions of the specified channel. | `c572876188918349857` |
| {u&lt;snowflake&gt;} | Will censor mentions of the specified user. | `u84912325282254848` |

### Antiraid Configuration
| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| count | Number of members that must join guild within `interval` to trigger antiraid. | int | 5 |
| interval | Seconds within which the `count` of members trigger the antiraid. | int | 60 |
| key\_duration | Seconds a user is remembered after joining. This should be larger than `interval`. | int | 600 |
| lockdown\_duration | Seconds that guild should be locked down with antiraid measures. | int | 600 |
| raidrole | Role ID applied to all users during antiraid measures.  | snowflake | empty |
| notifyrole | Role ID that should be notified when antiraid is automatically triggered | snowflake | empty |

**How antiraid works**

1. Antiraid measures are enabled once more then `count` number of joins are detected within `interval` seconds.
1. All users in the join table for the `key_duration` have the raidrole retroactively applied.
1. All users that join during `lockdown_duration` have the raidrole applied.
1. Antiraid measures will expire once less than `count` number of joins are detected within `interval` for  `lockdown_duration`.
1. Moderators will need to manually run `!raid disable` to remove all raid roles from remaining users.

The [modlogs plugin](modlog.md) will need to be configured with `RAID` logs for proper `notifyrole` alerts.

## Configuration Example

```yaml
plugins:
  censor:
    levels:
      50:
        filter_zalgo: true
        filter_invites: true
        invites_guild_whitelist: 
          - 205769246008016897 # Guild 1
          - 272885620769161216 # Guild 2
        invites_whitelist: 
          - discord-developers
          - discord-testers
          - discord-api
          - events
          - discord-linux
          - gamenight
          - discord-feedback
        filter_domains: true
        domains_blacklist: 
          - website.com
          - weirdlink.net
        blocked_tokens: 
          - token1
          - token2
        blocked_words: 
          - word1
          - word2
          - word3
        blocked_mentions: 
          - u84912325282254848
          - r579304983896391680
          - c572876188918349857
        blocked_nicknames: [blurb]
        zalgo_channel_whitelist: [510413274060161024]
        invites_channel_whitelist: [510413274060161024]
        domains_channel_whitelist: [510413274060161024]
        words_channel_whitelist: [510413274060161024]
        char_limit_channel_whitelist: [510413274060161024]
        mention_channel_whitelist: [510413274060161024]
        mute_violations: true
        mute_violations_count: 5
        mute_violations_interval: 15
        mute_violations_duration: 600
        antiraid:
          key_duration: 300
          interval: 30
          count: 3
          lockdown_duration: 300
          raidrole: 538720817773805569
          notifyrole: 536728730714898442
    channels:
      290923757399310337:
        blocked_words: [word4]  
  infractions:
    mute_role: 579398816072073246
```