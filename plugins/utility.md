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
| `!info {user}` | Returns information on the given user | Default | `!info 520047158104424488` OR `!info @HepBoat#0361` |
| `!jumbo {emojis}` | Returns 128x128px images of the given emoji | Default | `!jumbo :cat: :dog: :rabbit:` |
| `!random coin` | Flips a coin and returns the result | Default | `!random coin` |
| `!random number [end number] [start number]` | Returns a random number from 0-10 or in a range if specified | Default | `!random number` OR `!random number 50 20` |
| `!r add {duration} {content}` OR `!remind {duration} {content}` | Adds a reminder. Bot will mention the user after the specified duration with the given message | Default | `!r add 24h update announcements` OR `!remind 24h update announcements` |
| `!r clear` | Clears all of the user's reminders | Default | `!r clear` |
| `!search {query}` | Searches for usernames that match given query. If the result is the only object returned it will turn into info automatically | Default | `!search Alchameth` |
| `!seen {user}` | Returns the timestamp of when the bot last saw a message from given user | Default | `!seen 148359099782791168` OR `!seen @JakeyPrime` |
| `!server [guild]` | Returns information on the current server or the Server ID if given | Default | `!server` OR `!server 532372609476591626` |
| `!avatar {user}` | Displays user's avater | Default | `!avatar JakeyPrime` |
| `!announce {channel} {message}` | Announce message to channel. Channel must have configuration in the utility plugin configuration | Admin | `!announce #community-news it's a me, mario!` |
| `!docs` | Returns a list to view documentation | Default | `!docs`
| `!about` | Returns a list of servers and uptime | Default | `!about`
| `!help` | Returns an embed with a documentation link and homepage | Default | `!help`
| `!uptime` | Returns uptime command | Default | `!uptime` 
| `!ping` | Returns a phrase to indicate bot responsiveness | Default | `!ping` 

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

# Info Command Badges explanation

### Staff

![dev](https://cdn.discordapp.com/attachments/466804131965829130/576683733894037514/534956228816797697.png) - HepBoat Developer - Staff

![Support Team](https://cdn.discordapp.com/attachments/466804131965829130/576683725929316361/575946300638625792.png) - Support Team - Staff

![Support God](https://cdn.discordapp.com/attachments/466804131965829130/576683725929316361/575946300638625792.png) - HepBoat Support God - Staff

### Donators

![Reddit](https://cdn.discordapp.com/attachments/466804131965829130/576683736364744716/575965161333194753.png)- Discordapp Reddit Team - Not Staff

Donor - Base donor tier to show donor section profile, added when people donate

Nitro Booster - For the booster peeps once it launchers, given when someone boosts the server

![Donor 1](https://cdn.discordapp.com/attachments/466804131965829130/576683732740866048/575971423269683200.png) - Tiers of one time donations, separate from premium program SoonTM
 
![Donor 2](https://cdn.discordapp.com/attachments/466804131965829130/576683731603947521/575971422204067840.png) - Tiers of one time donations, separate from premium program SoonTM  
 
![Donor 3](https://cdn.discordapp.com/attachments/466804131965829130/576683729699864576/575971421939826706.png) - Tiers of one time donations, separate from premium program SoonTM   

![Donor 4](https://cdn.discordapp.com/attachments/466804131965829130/576683728483516446/575971421960929282.png) - Tiers of one time donations, separate from premium program SoonTM    
 
![Donor 5](https://cdn.discordapp.com/attachments/466804131965829130/576683727221030912/575972858514112512.png) - Tiers of one time donations, separate from premium program SoonTM  
  
![Sponsor](https://cdn.discordapp.com/attachments/466804131965829130/576683727221030912/575972858514112512.png) - Sponsor; Someone who greatly contributes towards the bot

### Automatic

![Global Admin](https://cdn.discordapp.com/attachments/466804131965829130/576683733894037514/534956228816797697.png) -  Global Administrator of HepBoat

![Hydra Server Admin](https://cdn.discordapp.com/attachments/466804131965829130/576683725929316361/575946300638625792.png) - Administrator of the Team Hydra Discord Server

![Hydra Server Mod](https://cdn.discordapp.com/attachments/466804131965829130/576683725929316361/575946300638625792.png) - Moderator of the Team Hydra Discord Server        

![Zira Premium](https://cdn.discordapp.com/attachments/466804131965829130/576683724259983370/549209441220952064.png) - Premium Users of Zira bot

Server Owner - Owner of a server using HepBoat        

User - User of HepBoat    

HepBoat Tester - Beta Testers for hepboat, automatically given when in a beta config.

![HepBoat Design Team](https://cdn.discordapp.com/attachments/576329728441581568/580774469212307456/575946300638625792.png) - For Team Hydra designers

HepBoat Volunteer Helper - For users that volunteer to help with the development of the bot




## Autoclean  Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| timeout | Time to wait before deleting \(seconds\) | int | None |

## Reaction Roles Configuration Options

## [Zira](https://zira.ovh/)

The reaction role function was removed due to high load on the bot. However, if you'd still like to use reaction roles, our dedicated bot for that [Zira](https://zira.ovh/) is an amazing choice with rich features and fast responsiveness. Join the [Team Hydra Discord Server](https://discordapp.com/invite/2wP2yjy) to learn more.

## Configuration Example

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