# Censor Plugin

Plugin name: `censor`

The censor plugin provides administrators and moderators a simple way to filter certain types of malicious and offensive content, such as:

* Invite Links
* URLs
* Inappropriate or offensive words (attachment names included)

This plugin combined with the Spam plugin can result in a very robust automatic abuse-prevention system.

## Commands

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Default Level</th>
      <th style="text-align:left">Usage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><code>!antiraid</code>
        </p>
        <p>OR</p>
        <p><code>!raid</code>
        </p>
      </td>
      <td style="text-align:left">Show if antiraid measures are active.</td>
      <td
      style="text-align:left">Moderator</td>
        <td style="text-align:left">
          <p><code>!antiraid</code> OR</p>
          <p><code>!raid</code>
          </p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>!raid disable</code>
        </p>
        <p>OR</p>
        <p><code>!antiraid disable</code>
        </p>
      </td>
      <td style="text-align:left">Disable antiraid and remove the raidrole role from all members.</td>
      <td
      style="text-align:left">Moderator</td>
        <td style="text-align:left"><code>!raid disable</code>
        </td>
    </tr>
  </tbody>
</table>

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| levels | A mapping of levels to Censor Configurations. This will match any user with a level that is equal or lower. | dict | empty |
| channels | A mapping of channels to Censor Configurations. | dict | empty |

### Censor Configuration

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| filter\_zalgo | Whether to filter zalgo text from messages | bool | true |
| filter_all_caps | Whether to filter messages that are all capital letters | bool | false /\
| filter\_invites | Whether to filter invite links from messages | bool | true |
| invites\_guild\_whitelist | A list of whitelisted guild IDs for invite codes | list(str) | empty |
| invites\_whitelist | A list of whitelisted invite codes or vanities | list(str) | empty |
| invites\_blacklist | A list of blacklisted invite codes or vanities | list(str) | empty |
| filter\_domains | Enables or disables domain filtering functionality. only `domains_whitelist` or only `domain_blacklist` will be checked. whitelist over blacklist. | bool | true |
| domains\_whitelist | A whitelist of domain names | list(str) | empty |
| domains\_blacklist | A blacklist of domain names | list(str) | empty |
| blocked\_tokens | A list of tokens \(can appear in the middle of words\) that are blacklisted. Also includes attachment names. | list(str) | empty |
| blocked\_words | A list of words \(must be separated by a boundary\) that are blacklisted. Also includes attachment names. | list(str) | empty |
| blocked\_mentions | A list of blacklisted mentions. Can work for channels, roles, or users. `c572876188918349857` for channel mention censor, `u84912325282254848` for user mention censor, `r579304983896391680` for role mention censor. | list(str) | empty | 
| blocked\_nicknames | A list of names \(can appear in the middle of nicknames\) that are blacklisted | list(str) | empty |
| block\_zalgo\_nicknames | Whether to filter nicknames with zalgo text | bool | false |
| message\_char\_limit | Maximum allowed message length | int | 0 |
| all_caps_min_char_length | minimum length of all caps to filter | int | 5 |
| warn\_on\_censor | Whether to automatically warn a user when their name or message is censored | bool | false |
| zalgo\_channel\_whitelist | Array of channels to whitelist for zalgo messages | list(snowflake) | empty |
| invites\_channel\_whitelist | Array of channels to whitelist for invites | list(snowflake) | empty |
| domains\_channel\_whitelist | Array of channels to whitelist for domains | list(snowflake) | empty |
| words\_channel\_whitelist | Array of channels to whitelist for blocked words | list(snowflake) | empty |
| mention\_channel\_whitelist | Array of channels to whitelist for blocked mentions | list(snowflake) | empty | 
| char\_limit\_channel\_whitelist | Array of channels to whitelist for character limit | list(snowflake) | empty |
| all_caps_channel_whitelist | Array of channels to whitelist for character limit | list(snowflake) | empty | 
| mute\_violations | This is the only option that needs to be set to enable the feature. Mute a user after so many violations  | bool | false |
| mute\_violations\_count | Amount of violations before muting | int | 3 |
| mute\_violations\_interval | How much time the count of violations must occur within for the mute to be enforced | int | 10 |
| mute\_violations\_duration | How long to temp mute for in seconds | int | 300 |
| antiraid | Antiraid configuration | dict | None |

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
plugin:
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
        invites_blacklist: []
        filter_domains: true
        domains_whitelist: []
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
```

NOTE: Every censor configuration setting can be applied to either `levels` or `channels`