# Utility Plugin

Plugin name: `utilities`

The utility plugin provides a number of useful and fun commands and utilities.

## Commands

Arguments in `{}` are required. Arguments in `[]` are optional.

### Info
| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!docs` | Returns a list of documentation links. | Default | `!docs` |
| `!about` | Returns a list of servers the bot is in and current uptime. | Default | `!about` |
| `!help` | Returns an embed with a list of common moderation commands and documentation links. | Default | `!help` | 
| `!uptime` | Returns the current uptime. | Default | `!uptime` |
| `!ping` | Returns a phrase to indicate bot responsiveness. | Default | `!ping` |
| `!emoji {emoji}` | Returns information on the given emoji. | Default | `!emoji :smiley:` |
| `!info [user]` | Returns information on the calling or given user. | Moderator | `!info` OR `!info 520047158104424488` OR `!info @HepBoat#0361` |
| `!server [guild_id]` | Returns information on the calling or given server. | Default | `!server` OR `!server 532372609476591626` |
| `!avatar {user}` | Displays the given user's avatar. | Default | `!avatar JakeyPrime` |
| `!search {query}` | Returns a list of usernames that match the given query string. If the result is a single user, it will return `info` on the given user instead. | Moderator | `!search Alchameth` |
| `!seen {user}` | Returns the timestamp of when the bot last saw a message from given user in the guild. | Default | `!seen 148359099782791168` OR `!seen @JakeyPrime` |
| `!notseen [duration]` | Returns a list of users that the bot has not seen a message from in the given duration in the guild. Default duration is `1d`. Give integer durations are parsed in days. | Moderator | `!notseen 3` OR `!notseen 3h` |
| `!announce {channel} {message}` | Announces a message to the given channel. Channels used must be configured in the `announce` section of the utilities configuration. | Administrator | `!announce #community-news it's a me, mario!` |

### Utility
| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!r add {duration} {content}` OR `!remind {duration} {content}` | Adds a reminder. Bot will mention the user after the specified duration with the given message. | Default | `!r add 24h update announcements` OR `!remind 24h update announcements` |
| `!r clear` | Clears all of the calling user's reminders. | Default | `!r clear` |

### Fun
| Name | Description | Default Level | Usage |
| :--- | :--- | :--- | :--- |
| `!cat` OR `!kitty` OR `!kitteh` OR `!catto` | Returns a random image of a cat. | Default | `!cat` |
| `!doggo` OR `!pupper` OR `!dog` OR `!doggy` OR `!doggo`| Returns a random image of a dog. | Default | `!doggo` |
| `!bunny` OR `!rabbit` OR `!wabbit` OR `!bunnerz` | Returns a random image of a bunny. | Default | `!bunny` |
| `!duck` OR `!quack` | Returns a random image of a duck. | Default | `!duck` |
| `!floof` | Returns a random image of a cat, dog, duck, or bunny. | Default | `!floof` |
| `!jumbo {emojis}` | Returns 128x128px images of the given emoji | Default | `!jumbo :cat: :dog: :rabbit:` |
| `!random coin` | Flips a coin and returns the result | Default | `!random coin` |
| `!random number [end number] [start number]` | Returns a random number from 0-10 or in a range if specified | Default | `!random number` OR `!random number 50 20` |

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| announce | Mapping of channel IDs to announce configurations. | dict | empty |
| auto\_clean | Mapping of channel IDs to autoclean configurations. | dict | empty |
| channels | Mapping of channel names or IDs to channel filtering configurations. | dict | empty|

### Announce Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| webhook\_id | ID of webhook to post to. | str | empty |
| webhook\_color | Color of webhook embed. | int | 0x000000 |
| webhook\_name | Username for webhook. | str | Guild name |
| webhook\_avatar | Avatar URL for the webhook. | str | empty |

### Autoclean Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| timeout | Seconds to wait before deleting | int | empty |

### Channel Filtering Configuration Options

NOTE: The [censor plugin](censor.md) and [infractions plugin](infractions.md) must be enabled in conjunction in order to use this feature.

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| allow_images | Whether to allow image uploads to the channel. | bool | true |
| allow_misc_files | Whether to allow non-image uploads to the channel. | bool | true |
| need_caption | Whether to require captions on image/file uploads. | bool | false |
| allow_text | Whether to allow plain text messages to the channel. | bool | true |
| whitelist_text_regex | A whitelisting regex that is run on the text content of every message in the channel. | str | empty |
| role_whitelist | A list of role IDs that will not have messages run through the filter. | list(snowflake) | empty |
| warn_on_censor | Whether to automatically warn a user when their message is censored. | bool | false |
| mute\_violations | Enable ability to mute a user after a set number of violations in the channel.  | bool | false |
| mute\_violations\_count | Number of violations that can be accrued in the channel in `mute_violations_interval` before muting. | int | 3 |
| mute\_violations\_interval | Seconds within which a user with over `mute_violations_count` violations in the channel will trigger a mute. | int | 10 |
| mute\_violations\_duration | Seconds to mute a user with sufficient violations in the channel. | int | 300 |

#### Whitelisting regex examples

To only allow messages that contain the phrase bunny somewhere:
```text
whitelist_text_regex: 'bunny'
```

To only allow single custom emote messages:
```text
whitelist_text_regex: '^<a?:\w+:[0-9]+>$'
```

To only allow messages consisting only of custom emotes and whitespace:
```text
whitelist_text_regex: '^(\s*<a?:\w+:[0-9]+>\s*)+$'
```

### Reaction Role Configuration Options

The reaction role configuration was removed due to high load on the bot. However, if you would still like to use reaction roles, our dedicated bot [Zira](https://zira.ovh/) is an amazing choice with rich features and fast responsiveness. Join the [Team Hydra Discord Server](https://discordapp.com/invite/2wP2yjy) to learn more.

## Configuration Example

```yaml
plugins:
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
    channels:
      579304983896391682:
        allow_images: false
        allow_text: true
        warn_on_censor: true
        mute_violations: true
        mute_violations_count: 2
        mute_violations_duration: 5
  infractions:
    mute_role: 579398816072073246
  censor: {}
```

## Info Badges
The following are a list of badges in the `info` command with explanations. 

### HepBoat Staff
| Image | Name | Description | 
| :--- | :--- | :--- |
| ![Global Admin](https://cdn.discordapp.com/attachments/466804131965829130/576683733894037514/534956228816797697.png) |  HepBoat Global Administrator | For HepBoat global administrators. |
| ![Developer](https://cdn.discordapp.com/attachments/466804131965829130/576683733894037514/534956228816797697.png) | HepBoat Developer | For HepBoat code developers. |
| ![Server Administrator](https://cdn.discordapp.com/attachments/466804131965829130/576683725929316361/575946300638625792.png) | HepBoat Server Administrator | For administrators on the support server. |
| ![Server Moderator](https://cdn.discordapp.com/attachments/466804131965829130/576683725929316361/575946300638625792.png) | HepBoat Server Moderator | For moderators on the support server. |
| ![Support God](https://cdn.discordapp.com/attachments/466804131965829130/576683725929316361/575946300638625792.png) | HepBoat Support God | For support staff on the support server. |
| ![Support Team](https://cdn.discordapp.com/attachments/466804131965829130/576683725929316361/575946300638625792.png) | Hepboat Support Team | For support staff on the support server. |

### HepBoat Supporter
| Image | Name | Description | 
| :--- | :--- | :--- |
| | HepBoat Supporter | |
| ![Donor 1](https://cdn.discordapp.com/attachments/466804131965829130/576683732740866048/575971423269683200.png) | HepBoat Supporter Tier 1 | |
| ![Donor 2](https://cdn.discordapp.com/attachments/466804131965829130/576683731603947521/575971422204067840.png) | HepBoat Supporter Tier 2 |  | 
| ![Donor 3](https://cdn.discordapp.com/attachments/466804131965829130/576683729699864576/575971421939826706.png) | HepBoat Supporter Tier 3 |  |    
| ![Donor 4](https://cdn.discordapp.com/attachments/466804131965829130/576683728483516446/575971421960929282.png) | HepBoat Supporter Tier 4 |  |    
| ![Donor 5](https://cdn.discordapp.com/attachments/466804131965829130/576683727221030912/575972858514112512.png) | HepBoat Supporter Tier 5 |  | 
| ![Sponsor](https://cdn.discordapp.com/attachments/466804131965829130/576683727221030912/575972858514112512.png) | HepBoat Sponsor & Absolute Wonderful Person | For users who greatly contribute towards the bot. |
| | HepBoat Volunteer Helper | For users that volunteer to help with HepBoat development. |
| | HepBoat Volunteer Guru | |

### User
| Image | Name | Description | 
| :--- | :--- | :--- |
|![Reddit](https://cdn.discordapp.com/attachments/466804131965829130/576683736364744716/575965161333194753.png) | r/DiscordApp Official Reddit Mod | Moderator on r/discordapp, not necessarily Discord staff or Hepboat staff. |
| ![Design Team](https://cdn.discordapp.com/attachments/466804131965829130/576683725929316361/575946300638625792.png) | HepBoat Design Team | For designers in Team Hydra. |
|![Nitro Booster](https://cdn.discordapp.com/emojis/588291355797749760.png) | Team Hydra Nitro Booster | For users that have boosted the support guild. |
| ![Partner](https://cdn.discordapp.com/emojis/540660679758184469.png) | Team Hydra Partner | For partners with Team Hydra.|
| ![Zira Premium](https://cdn.discordapp.com/attachments/466804131965829130/576683724259983370/549209441220952064.png) | Zira Premium | For premium users of the [Zira](https://zira.ovh/) bot. | 
| | Verified HepBoat Server Owner | Automatically given to owners of servers with HepBoat. |
| | Verified HepBoat User | Automatically given to users in the `web` section of any HepBoat configuration file. |
| | HepBoat Beta Tester | Automatically given to users in the `web` section of any HepBoat Beta configuration file.|
