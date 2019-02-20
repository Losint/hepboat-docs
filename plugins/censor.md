# Censor Plugin

The censor plugin provides administrators and moderators a simple way to filter certain types of malicious and offensive content, such as:

* Invite Links
* URLs
* Inappropriate or Offensive words

This, combined with the Spam plugin can result in a very robust automatic abuse-prevention system.

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| levels | A mapping of levels to Censor Configurations. This will match any user with a level that is equal or lower | dict | empty |
| channels | A mapping of channels to Censor Configurations | dict | empty |

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
        <p><code>!antiraid </code>
        </p>
        <p>OR</p>
        <p><code>!raid</code>
        </p>
      </td>
      <td style="text-align:left">Without arguments antiraid/raid will show if antiraid measures are active.</td>
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
      <td style="text-align:left">Remove the measures and remove the raidrole role from all members.</td>
      <td
      style="text-align:left">Moderator</td>
        <td style="text-align:left"><code>!raid disable</code>
        </td>
    </tr>
  </tbody>
</table>## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| levels | A mapping of levels to Censor Configurations. This will match any user with a level that is equal or lower | dict | empty |
| channels | A mapping of channels to Censor Configurations | dict | empty |

### Censor Configuration

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| filter\_zalgo | Whether to filter zalgo text from messages | bool | true |
| filter\_invites | Whether to filter invite links from messages | bool | true |
| invites\_guild\_whitelist | A list of whitelisted guild IDs for invite codes | list | empty |
| invites\_whitelist | A list of whitelisted invite codes or vanities | list | empty |
| invites\_blacklist | A list of blacklisted invite codes or vanities | list | empty |
| filter\_domains | Whether to filter the domains contained within URLs. Enables or disables domain filtering functionality. | bool | true |
| domains\_whitelist | A whitelist of domain names | list | empty |
| domains\_blacklist | A blacklist of domain names | list | empty |
| blocked\_tokens | A list of tokens \(can appear in the middle of words\) that are blacklisted | list | empty |
| blocked\_words | A list of words \(must be seperated by a boundary\) that are blacklisted | list | empty |
| blocked\_nicknames | A list of names \(can appear in the middle of nicknames\) that are blacklisted | list | empty |
| block\_zalgo\_nicknames | Whether to filter nicknames with zalgo text | bool | false |
|  message\_char\_limit | Maximum allowed message length | int | 0 |
| warn\_on\_censor | Whether to automatically warn a user when their name or message is censored | bool | false |
| zalgo\_channel\_whitelist | Array of channels to whitelist for zalgo messages | id array | empty |
| invites\_channel\_whitelist | Array of channels to whitelist for invites | id array | empty |
| domains\_channel\_whitelist | Array of channels to whitelist for domains | id array | empty |
| words\_channel\_whitelist | Array of channels to whitelist for blocked words | id array | empty |
| char\_limit\_channel\_whitelist | Array of channels to whitelist for character limit | id array | empty |
| mute\_violations | This is the only option that needs to be set to enable the feature. Mute a user after so many violations  | bool | false |
| mute\_violations\_count | Amount of violations before muting | int | 3 |
| mute\_violations\_interval | How much time the count of violations must occur within for the mute to be enforced | int | 10 |
| mute\_violations\_duration | How long to temp mute for in seconds | int | 300 |
| antiraid | Antiraid subconfig | dict | None |

### Antiraid Configuration

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| count | Number of members that must join guild within the 'duration' to trigger antiraid | int | 5 |
| interval | Time period within which the "count" of members trigger the antiraid in seconds | int | 60 |
| key\_duration | How many seconds a user that has joined is remembered. This is used when antiraid is triggered and will apply the 'raidrole' to. This should be larger than the interval e.g 300 seconds / 600 seconds etc | int | 600 |
| lockdown\_duration | How many seconds after antiraid has been enabled should all further members that join the server have the 'raidrole' applied. | int | 600 |
| raidrole | Snowflake value of a role that should be applied first to all users currently in 'key\_duration' then subsequent members joining within 'lockdown\_duration'  | snowflake | empty |
| notifyrole | Snowflake value of a role that should be notified when antiraid is automatically triggered | snowflake | empty |

## Configuration Example

```yaml
  censor:
    levels:
      50:
        filter_zalgo: true
        filter_invites: true
        invites_guild_whitelist: [205769246008016897, 272885620769161216]
        invites_whitelist: ['discord-developers', 'discord-testers', 'discord-api', 'events', 'discord-linux', 'gamenight', 'discord-feedback']
        invites_blacklist: []
        filter_domains: true
        domains_whitelist: []
        domains_blacklist: ['website.net']
        blocked_tokens: ['token1', 'token2']
        blocked_words: ['word1', 'word2', 'word3']
        blocked_nicknames: ['blurb']
        zalgo_channel_whitelist: [510413274060161024]
        invites_channel_whitelist: [510413274060161024]
        domains_channel_whitelist: [510413274060161024]
        words_channel_whitelist: [510413274060161024]
        char_limit_channel_whitelist: [510413274060161024]
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
        blocked_words: ['word4']
```

Note: Every censor configuration setting can be applied to either `levels` or `channels`