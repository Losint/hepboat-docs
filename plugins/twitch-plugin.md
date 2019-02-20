# Twitch Plugin

The twitch plugin provides an advanced system to announce twitch streams within your guild. Two major options exist where the first is the traditional method of defining a list of streams to announce when they are live, the second method allows for dynamic stream announcements based off members of your guild who are streaming.

This includes the dynamic assignment of roles which can be used to hoist currently streaming members higher in the guild member list. Other options include custom message announcements, and basic regex for stream title and game to ensure only specified streams are announced for your guild.

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| configs | Dict of configurations for channels | Dict | None |
| ignore\_users | Snowflake list of ignored users for all configs | snowflake list | \[\] |

## Configs Options

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Default</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">stream_role</td>
      <td style="text-align:left">Users that belong to this role id will be considered as part of the stream
        announcement (tip use <code>!roles</code> to find the id to use)</td>
      <td
      style="text-align:left">snowflake</td>
        <td style="text-align:left">None</td>
    </tr>
    <tr>
      <td style="text-align:left">add_roles</td>
      <td style="text-align:left">List of role id's that will be added to the user when streaming. This
        can be used to hoist the users for example</td>
      <td style="text-align:left">snowflake list</td>
      <td style="text-align:left">[]</td>
    </tr>
    <tr>
      <td style="text-align:left">ignore_roles</td>
      <td style="text-align:left">List of role id's that will be ignored, even if the user belongs to the
        stream_role</td>
      <td style="text-align:left">snowflake list</td>
      <td style="text-align:left">[]</td>
    </tr>
    <tr>
      <td style="text-align:left">ignore_users</td>
      <td style="text-align:left">List of user id's that will be ignored for this channel, even if the user
        belongs to the stream_role</td>
      <td style="text-align:left">snowflake list</td>
      <td style="text-align:left">[]</td>
    </tr>
    <tr>
      <td style="text-align:left">message</td>
      <td style="text-align:left">
        <p>Custom announce message. The following tokens can be used:</p>
        <p><code>{user}</code> Streamers username</p>
        <p><code>{here}</code> @here</p>
        <p><code>{everyone}</code> @everyone</p>
        <p><code>{r123456789012}</code> @role</p>
        <p>Custom role id must follow the letter `r`</p>
      </td>
      <td style="text-align:left">str</td>
      <td style="text-align:left">None</td>
    </tr>
    <tr>
      <td style="text-align:left">no_embed</td>
      <td style="text-align:left">If set to <code>True</code> no embed will be used in the announcement. Only
        the message will be shown</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">False</td>
    </tr>
    <tr>
      <td style="text-align:left">notification_type</td>
      <td style="text-align:left">
        <p>Either set to the following which will announce to the specified:</p>
        <p><code>HERE</code> @here</p>
        <p><code>EVERYONE</code> @everyone</p>
        <p><code>ROLE</code> Specific role defined in notification_target option</p>
      </td>
      <td style="text-align:left">Enum</td>
      <td style="text-align:left">None</td>
    </tr>
    <tr>
      <td style="text-align:left">notification_target</td>
      <td style="text-align:left">Snowflake roleid of custom role to announce to when notification_type
        is set to ROLE</td>
      <td style="text-align:left">snowflake</td>
      <td style="text-align:left">None</td>
    </tr>
    <tr>
      <td style="text-align:left">title_re</td>
      <td style="text-align:left">regex to be used on the stream title. This is case insensitive</td>
      <td
      style="text-align:left">str / regex</td>
        <td style="text-align:left">None</td>
    </tr>
    <tr>
      <td style="text-align:left">game_re</td>
      <td style="text-align:left">
        <p>regex to be used on the game title.</p>
        <p>This is case insensitive</p>
      </td>
      <td style="text-align:left">str / regex</td>
      <td style="text-align:left">None</td>
    </tr>
    <tr>
      <td style="text-align:left">streams</td>
      <td style="text-align:left">List of stream names to subscribe to. When the stream is live it will
        announce</td>
      <td style="text-align:left">str list</td>
      <td style="text-align:left">None</td>
    </tr>
    <tr>
      <td style="text-align:left">channel_id</td>
      <td style="text-align:left">Channel id used if the config is set to a unicode string. This allows
        the same channel to have multiple configurations by having different unicode
        string configs</td>
      <td style="text-align:left">snowflake</td>
      <td style="text-align:left">None</td>
    </tr>
  </tbody>
</table>## Configuration Example

### Basic Stream Subscribe Example

The following example is a basic example of subscribing to a list of streams that will be announced to a channel when live.

```yaml
twitch:
  configs:
    297917022300274688:
      streams:
        - warframe
        - discordapp
        - JakeyPrimed
```

### Advanced Example

The following example is based off the following conditions:

* Everyone should be announced if they meet below conditions
* Only for the game Warframe
* A custom message and announce to custom role
* A specific role is excluded
* A specific role is added when streaming

```yaml
twitch:
  configs:
    297917022300274688:
      stream_role: 146691885363232769 # everyone role
      ignore_roles:
        - 748393947474923485 # Naughty people
      add_roles:
        - 544172349474340868 # Currently Streaming
      game_re: 'warframe'
      message: |-
        {r1234567890122334} {user} is being totally awesome and
        streaming right now you should check it out!!
```

It should be noted that it is also possible to specify the configs as a unicode string thus allowing multiple configurations for the same channel as follows:

```yaml
twitch:
  configs:
    devstream:
      channel_id: 297917022300274688
      streams:
        - warframe
      title_re: 'devstream'
      message: |-
        DevStream is now live!
    ps4:
      channel_id: 297917022300274688
      streams:
        - warframe
      title_re: 'ps4 @ 4'
      message: |-
        PS4 @ 4 is now live!
    xbox:
      channel_id: 297917022300274688
      streams:
        - warframe
      title_re: 'xbox one @ 1'
      message: |-
        XB1 @ 1 is now live!
```

## Notes

The twitch plugin requires an option to be set in the `config.yaml` for the twitch client ID API key.

```yaml
stream:
  TWITCH_CLIENT_ID: '987dfs876876978sdf8799'
```

Announces can only occur once per hour per user into a channel. If the stream is not restarted after the hour it will not re-announce.

