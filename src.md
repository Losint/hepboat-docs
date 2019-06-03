# What is HepBoat

HepBoat is a fork of b1nzy's rowboat, a utilitarian and administration assistant for Discord. It iss a bot that was built to be highly configurable and allow server admins to modify functionality based on the requirements of individual servers. 

The freely-hosted Hepboat is private and closed-source. It is only added on high-traffic servers. Rowboat is open-source with public code.

## Use Cases

#### Multiple Mod Logs

Admins are able to split and categorize logs into various channels and reduce noise without sacrificing logging.

#### Spam Prevention

By turning on spam prevention, HepBoat takes a huge burden off moderators and ensures the server is safe even when nobody is watching. With its high level of configurability, it is able to ensure a level of security which does not impact normal chat but catches bad actors quickly and efficiently.

#### Censoring 

By enabling Hepboat's advanced censor plugin, you can choose from a wide array of options to filter certain types of malicious and offensive content, such as invite links, domains, and inappropriate or offensive words. When combined with the spam plugin, it is a very capable automated moderation system. 

## User Testimonials

### Looney - Events and Community for Discord

> Rowboat has allowed us to efficiently scale the moderation teams of our large public and private community servers, without placing extra burden on our volunteer moderators or sacrificing auditability.

## Plugins

* Administration
  * Banning, kicking, muting
  * Managing and tracking infractions and reasons per user and moderator
  * User persistence \(resetting roles/nickname/voice settings when users leave and rejoin\)
  * Chat cleaning and archiving
  * Chat slow mode and chat mute
  * Granular role management \(adding/removing roles\)
  * Role tracking and info
  * Invite pruning
  * Reactions pruning
  * Voice activity log
  * Mobile moderation function
* Spam
  * Highly configurable spam thresholds which can help block:
    * Message spam
    * Mention spam
    * Link spam
    * Emoji spam
    * Newline/large message spam
    * Attachment/upload spam
    * Duplicated message spam / raids
  * Per-rule and global punishment configuration that can ban, tempban, mute, tempmute, or kick users
  * Auto-cleaning of messages based on rules
  * Ability to whitelist channels per spam type or per server
* Censor
  * Zalgo prevention
  * Whitelisting of invites based on vanity url or destination server
  * Whitelisting of URLs and domains
  * Filtering of words and tokens (even on attachment names!)
  * Ability to whitelist channels from zalgo, invite, domain, character limit filters
  * Level based configuration granularity
  * User nickname filtering
  * Automated mute based on word censoring
  * Raid Prevention
  * User, role, and channel mention prevention
* Mod Log
  * Granular logging of events
  * Support for multiple channels
  * Ability to include exact timestamps in specific timezone (in plain text mode)
  * Ignore actions of specific users
  * Ignore actions in specific channels (helpful for moderation-only channels)
  * Highlighting newly created accounts on join
  * Support for automatic batching during high-throughput periods \(user purges, raids, cleans, etc\) that prevents log messages from backing up
  * Support for either fully customized moderation log format or embedded format
* Tags
  * Create custom responses that respond to a customized command name
  * Ability to restrict tag usage and creation to user level, role, or channel
* Utilities
  * Long-term persistent reminders
  * Random number and coin generation
  * User information, including last seen time
  * Server, user, avatar, emoji information
  * User search
  * Announcement function
  * Auto-clean timed function for channel
  * CAT PHOTOS
  * DOGGO PHOTOS AND GIFS
  * BUNNY GIFS
  * DUCK PHOTOS AND GIFS
* Custom Commands
  * Creation of power custom commands upon manual trigger or certain strings and commands
  * Custom commands can be a simple message or emoji response to a chain of commands
  * Ability to lock commands to a certain role or channel
* Autolevels
  * Whitelisting channels for points to be awarded
  * Whitelisting roles for points to be awarded
  * Ability to include voice chats and award points per time spent
  * Ability to customize points awarded per message and cooldown
  * Ability to have multiple level systems per category with different point award
  * Ability to add multiplier on messages, voice activity, or certain roles
  * Ability to add weight to messages, thus varying the awarded value in a range
  * Ability to award roles per set levels, fully configurable
  * Ability to keep previous roles or not
  * Ability to announce level ups in a channel, or DMs, and fully custom messages
* Reddit
  * Support for multiple subreddit sources and channel destinations
  * Support for including post stats
  * Support for filtering nsfw content
  * Support for moderator feeds
  * Ability to ping role per post
* Starboard
  * Highly configurable
  * In-depth stats and leaderboard
  * Ability to entirely block users from starboard
  * Ability to lock/unlock starboard on-demand
* Twitch notifications
  * Announcement of streams with fully configurable settings such as below 
  * Fully custom announce message
  * Roles to announce to
  * Adding a role to the streaming user
  * Ignoring a certain role or users, thus not announcing to them
  * Filtering announced streams based on stream title 
  * Filtering announced streams based on streamed game
  * Support for multiple announcement channels and streams.  
