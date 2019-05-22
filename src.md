# What is HepBoat

HepBoat is a fork of b1nzy's rowboat, a utilitarian and administration assistant for Discord. It's a bot that was built to be highly configurable, and allow server admins to modify functionality based on the requirements of individual servers. The freely hosted version of Rowboat is private, and only added on high-traffic servers. HepBoat is open-source.

## Use Cases

#### Multiple Mod Logs

By using Rowboat's support for multiple mod logs, admins are able to split and categorize logs into various channels, reducing noise without sacrificing logging.

#### Spam Prevention

By turning on spam prevention, HepBoat takes a huge burden off moderators and ensures the server is safe even when nobody is watching. With the high level of configurability it is able to ensure a level of security which does not impact normal chat, but catches bad actors quickly and efficiently.

#### Censoring 

By enabling Hepboat's advanced censor plugin, you will be able to choose from a wide array of options to filter certain types of malicious and offensive content, such as invite links, domains, and inappropriate or offensive words. When combined with the aforementioned Spam plugin, it is a very prominent, automated moderation system. 

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
* Censor
  * Zalgo prevention
  * Whitelisting of invites based on vanity url or destination server
  * Whitelisting of URLs and domains
  * Filtering of words and tokens
  * Ability to whitelist channels from zalgo, invite, domain, character limit filters
  * Level based configuration granularity
  * User nickname filtering
  * Automated mute based on word censoring
  * Raid Prevention
* Mod Log
  * Granular logging of events
  * Support for multiple channels
  * Ability to include exact timestamps in specific timezone
  * Ignoring and filtering of specific users \(helpful for music/etc bots\)
  * Ignoring and filtering of specific channels \(helpful for moderation only channels\)
  * Highlighting newly created accounts on join
  * Support for automatic batching during high-throughput periods \(user purges, raids, cleans, etc\) prevents log messages from backing up
  * Support for either fully customized moderation log format or embedded format
* Reddit
  * Support for multiple subreddit sources and channel destinations
  * Support for including post stats
  * Support for filtering nsfw content
  * Ability to ping role per post
* Spam
  * Highly configurable spam thresholds which can help block:
    * Message Spam
    * Mention Spam
    * Link Spam
    * Emoji Spam
    * Newline/Large Message Spam
    * Attachment/Upload Spam
    * Duplicated Message Spam / Raids
  * Per-rule and global punishment configuration can ban, tempban, mute, tempmute, or kick users
  * Auto-cleaning of messages based on rules
  * Ability to whitelist channels per spam type or per server
* Starboard
  * Highly configurable
  * In-depth stats and leaderboard
  * Ability to entirely block users from starboard
  * Ability to lock/unlock starboard on-demand
* Utilities
  * Long-term persistent reminders
  * Random number and coin generation
  * User information, including last seen time
  * Server, user, avatar, emoji information
  * User search
  * Announcement function
  * Auto-clean timed function for channel
  * CAT PHOTOS
  * DOGGO PHOTOS
  * BUNNY PHOTOS
  * Command for one of the above, randomly.
* Tags
  * Custom command responses that respond to a set command
  * Ability to create, delete, and remove \(mod only\) tags
  * Ability to restrict tags to user level, role, or channel
* Custom Commands
  * Creation of power custom commands
  * Custom commands can be a simple response, or a chain of commands
  * Locking commands to a certain role or channel
* Levels
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
* Twitch notifications
  * Announcement of streams with fully configurable settings such as below 
  * Fully custom announce message
  * Roles to announce to
  * Adding a role to the streaming user
  * Ignoring a certain role or users, thus not announcing to them
  * Filtering announced streams based on stream title 
  * Filtering announced streams based on streamed game
  * Support for multiple announcement channels and streams.  
