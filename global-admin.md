# Global Admin / Dev Handbook

This page will show commands and functionality that is meant only for developers, or global admins, and each will be documented as such. If you fell upon this page by accident, you're welcome to stay for tea.

There is some functionality you have to enable via command line, such as adding a global admin or other harmful commands these are completely reserved to JakeyPrime#0001, you can safely ignore these... This is only for Global Admins, and will serve as a handbook.

#### Whitelisting

| Command | Description | Note |
| :--- | :--- | :--- |
| !guilds wh  | Adds guilt to whitelist | Whitelist is temporary, if user does not add bot quick enough, they may need to be whitelisted again, contact me for this. |
| !guilds unwh | Removes guild from whitelist | This will not kick the bot, it will simply not allow them to add the bot in case of mistake or if you want they haven't invited yet. |


#### Add Or Remove Guild Flags

```
!guilds wh-add GUILD_ID FLAG
!guilds wh-rmv GUILD_ID FLAG
```

#### Valid Guild Flags

| Option | Description |
| :--- | :--- |
| `MODLOG_CUSTOM_FORMAT` | Allows the modlog custom format |
| `MUSIC` | Does nothing |
| `PREMIUM` | Should Not Be Used And Has Been Migrated To Redis |

#### Badges

The badge command can be used to either give or take away the badge, if someone already has the badge and you run this command it will also take it away. It works both ways, in a single command.

```
!badge USER_ID BADGE_ID
```

#### Badge Descriptions
Badges should only be given out by JakeyPrime, or automatically. If you feel someone deserves a badge, you may ask and be given permission to add said badge as soon as possible.

These are in ascending order based on what label they would appear under, etc.

| Badge | Badge Slug | Description Of Tag | Grant Type | How To Get |
| :--- | :--- | :--- | :--- | :--- |
| HepBoat Global Administrator | N/A | Bot Global Admin | RDB | Be Global Admin |
| HepBoat Developer | dev | Programmer for HepBoat | Command | Develop for HepBoat |
| HepBoat Server Administrator | N/A | Server Admin For Team Hydra | Role | Become Server Admin |
| HepBoat Server Moderator | N/A | Server Mod For Team Hydra | Role | Apply and become Server Mod | 
| HepBoat Support God | supportt4 | The Highest Support Role For The Elite | Command | Dedicate Your Life To The Boat | 
| HepBoat Support Team | supportt3 | First Tier Support Team Staff | Command | Part Of The Support Role |
| Donor | donor | Display Tag / Anyone Who Gives $ | Command | Donate any amount of money |
| Sponsor | sponsor | Top Tier Supporter Role | Command | Donate $100+ |
| Supporter Tier 5 | donor5 | Tier 5 Supporter | Command | Donate $80 - \$100 |
| Supporter Tier 4 | donor4 | Tier 4 Supporter | Command | Donate $60 - \$80 | 
| Supporter Tier 3 | donor3 | Tier 3 Supporter | Command | Donate $40 - \$60 | 
| Supporter Tier 2 | donor2 | Tier 2 Supporter | Command | Donate $20 - \$40 | 
| Supporter Tier 1 | donor1 | Tier 1 Supporter | Command | Donate $10 - \$20 | 
| HepBoat Volunteer Helper | supportt2 | For Helpful Volunteers | Command | After being a guru for a while |
| HepBoat Volunteer Guru | supportt1 | When a user helps and knows the boat | Command | Knowing enough about the boat | 
| r/DiscordApp Official Reddit Mod | reddit | For r/DiscordApp Reddit Mods ONLY | Command | Become a Reddit Mod? |
| HepBoat Design Team | N/A | Artists for Team Hydra Bots | Role | Make art for our bots |
| Team Hydra Nitro Booster | N/A | Granted when someone boosts server | Role | Nitro Boost Team Hydra | 
| Team Hydra Partner | N/A | Zira Partners | Role | Become a Zira / TH Partner | 
| Zira Premium | N/A | Zira Premium User | Role | Buy Zira Premium | 
| HepBoat Server Owner | N/A | Owns a HepBoat run server | RDB | Own a HepBoat run server | 
| HepBoat User | N/A | Role for being in a HepBoat Config | RDB | Be part of a HepBoat Run Server | 
| HepBoat Tester | N/A | Being in a part of a HBB test guild | RDB | Be part of a test server config |