# Utility Plugin

The utility plugin provides a number of useful and fun commands

## Commands

| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!cat / kitty / kitteh` | Returns a random image of a cat | Default | `!cat` OR `!kitteh` OR `!kitty` |
| `!doggo / pupper / dig / doggy` | Returns a random image of a dog | Default | `!doggo` |
| `!bunny` | Returns a random image of a bunny | Default | `!bunny` OR `!bunbun` |
| `!floof` | Returns a random image of a cat, dog or bunny | Default | `!floof` |
| `!emoji {emoji}` | Returns information on the given emoji | Default | `!emoji :smiley:` |
| `!info {user}` | Returns information on the given user | Default | `!info 232921983317180416` OR `!info @rowboat#0001` |
| `!jumbo {emojis}` | Returns 128x128px images of the given emoji | Default | `!jumbo :cat: :dog: :rabbit:` |
| `!random coin` | Flips a coin and returns the result | Default | `!random coin` |
| `!random number [end number] [start number]` | Returns a random number from 0-10 or in a range if specified | Default | `!random number` OR `!random number 50 20` |
| `!r add {duration} {content}` OR `!remind {duration} {content}` | Adds a reminder. Bot will mention the user after the specified duration with the given message | Default | `!r add 24h update announcements` OR `!remind 24h update announcements` |
| `!r clear` | Clears all of the user's reminders | Default | `!r clear` |
| `!search {query}` | Searches for usernames that match given query. If the result is the only object returned it will turn into info automatically | Default | `!search b1nzy` |
| `!seen {user}` | Returns the timestamp of when the bot last saw a message from given user | Default | `!seen 232921983317180416` OR `!seen @rowboat#0001` |
| `!server [guild]` | Returns information on the current server or the Server ID if given | Default | `!server` OR `!server 290923757399310337` |
| `!avatar {user}` | Displays user's avater | Default | `!avatar b1nzy` |
| `!announce {channel} {message}` | Announce message to channel. Channel must have configuration in the utility plugin configuration | Admin | `!announce #community-news it's a me, mario!` |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| announce | Channels that can be announced into | dict | empty |
| auto\_clean | Channels that can be autocleaned | dict | empty |

## Announce Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| webhook\_id | ID of webhook to post to | str | empty |
| webhook\_color | Color of webhook embed | int | 0x000000 |
| webhook\_name | Username for webhook | str | Guild Name |
| webhook\_avatar | Avatar URL for webhook "user" | str | None |

## Autoclean  Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| timeout | Time to wait before deleting \(seconds\) | int | None |

## Reaction Roles Configuration Options

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
      <td style="text-align:left">emoji</td>
      <td style="text-align:left">
        <p>Dict containing the emoji id and a list of role ids. (It is also possible
          to include an inbuilt emoji name in place of the emoji id)</p>
        <p>Also note that if one of the roles is set to either of below it will force
          that reaction to only allow join or leave of such roles:</p>
        <ul>
          <li><code>join_only</code>
          </li>
          <li><code>leave_only</code>
          </li>
        </ul>
      </td>
      <td style="text-align:left">dict</td>
      <td style="text-align:left">empty</td>
    </tr>
  </tbody>
</table>## Configuration Example

```yaml
utilities:
  announce:
    32490583480348083409:
      webhook_id: 304958304934209534
      webhook_color: 0xffffff
      webhook_name: HepBoat
      webhook_avatar: http://i.imjake.me/files/xoi30.png
  auto_clean:
    32490583480348083409:
      timeout: 3600
```