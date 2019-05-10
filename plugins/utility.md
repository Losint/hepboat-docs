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

## Info Command Badges explanation

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
<t>
  <th style="text-align:left">Staff</th>
</t>  
  <tbody>
    <tr>
      <td style="text-align:left">![dev](https://cdn.discordapp.com/emojis/534956228816797697.png?v=1)</td>
      <td style="text-align:left">
        <p>HepBoat Developer</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">![Support Team](https://cdn.discordapp.com/emojis/575946300638625792.png?v=1)</td>
      <td style="text-align:left">
        <p>HepBoat Support Team</p>
      </td>
    </tr> 
    <tr>
      <td style="text-align:left">![Support God](https://cdn.discordapp.com/emojis/575946300638625792.png?v=1)</td>
      <td style="text-align:left">
        <p>HepBoat Support God</p>
      </td>
    </tr> 
<t>
  <th style="text-align:left">User Titles</th>
</t>
    <tr>
      <td style="text-align:left">Helper</td>
      <td style="text-align:left">
        <p>HepBoat Helper - Not Staff</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Guru</td>
      <td style="text-align:left">
        <p>HepBoat Guru - Not Staff</p>
      </td>
    </tr> 
    <tr>
      <td style="text-align:left">![Reddit](https://cdn.discordapp.com/emojis/575965161333194753.png?v=1)</td>
      <td style="text-align:left">
        <p>Discordapp Reddit Team - Not Staff</p>
      </td>
    </tr>  
<t>
  <th style="text-align:left">Donor Tiers</th>
</t>     
    <tr>
      <td style="text-align:left">donor</td>
      <td style="text-align:left">
        <p>Base donor tier to show donor section profile, added when people donate</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">![Donor 1](https://cdn.discordapp.com/emojis/575971423269683200.png?v=1)</td>
      <td style="text-align:left">
        <p>Tiers of one time donations, separate from premium program SoonTM</p>
      </td>
    </tr> 
      <td style="text-align:left">![Donor 2](https://cdn.discordapp.com/emojis/575971422204067840.png?v=1)</td>
      <td style="text-align:left">
        <p>Tiers of one time donations, separate from premium program SoonTM</p>    
    <tr>
    </tr> 
      <td style="text-align:left">![Donor 3](https://cdn.discordapp.com/emojis/575971421939826706.png?v=1)</td>
      <td style="text-align:left">
        <p>Tiers of one time donations, separate from premium program SoonTM</p>    
    <tr>  
    </tr> 
      <td style="text-align:left">![Donor 4](https://cdn.discordapp.com/emojis/575971421960929282.png?v=1)</td>
      <td style="text-align:left">
        <p>Tiers of one time donations, separate from premium program SoonTM</p>    
    <tr> 
    </tr> 
      <td style="text-align:left">![Donor 5](https://cdn.discordapp.com/emojis/575972858514112512.png?v=1)</td>
      <td style="text-align:left">
        <p>Tiers of one time donations, separate from premium program SoonTM</p>    
    <tr>             
      <td style="text-align:left">![Sponsor](https://cdn.discordapp.com/emojis/575972858514112512.png?v=1)</td>
      <td style="text-align:left">
        <p>Big Boi</p>
      </td>
    </tr> 
<t>
  <th style="text-align:left">Automatic</th>
</t>
    <tr>
      <td style="text-align:left">![Global Admin](https://cdn.discordapp.com/emojis/534956228816797697.png?v=1)</td>
      <td style="text-align:left">Global Administrator of HepBoat
      </td>                
    <tr>
      <td style="text-align:left">![Hydra Server Admin](https://cdn.discordapp.com/emojis/575946300638625792.png?v=1)</td>
      <td style="text-align:left">Administrator of the Team Hydra Discord Server
      </td>
    <tr>
      <td style="text-align:left">![Hydra Server Mod](https://cdn.discordapp.com/emojis/575946300638625792.png?v=1)</td>
      <td style="text-align:left">Moderator of the Team Hydra Discord Server        
      </td> 
    <tr>
      <td style="text-align:left">Server Owner</td>
      <td style="text-align:left">Owner of a server using HepBoat        
      </td>  
    <tr>
      <td style="text-align:left">User</td>
      <td style="text-align:left">User of HepBoat      
      </td>                 
    </tr> 
  </tbody>
</table>


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
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">[Zira](https://zira.ovh/)</td>
      <td style="text-align:left">
        <p>The reaction role function was removed due to high load on the bot. However, if you'd still like to use reaction roles, our dedicated bot for that [Zira](https://zira.ovh/) is an amazing choice with rich features and fast responsiveness. Join the [Team Hydra Discord Server]() to learn more.</p>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

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