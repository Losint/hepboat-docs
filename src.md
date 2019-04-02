# What is HepBoat

HepBoat is a fork of b1nzy's rowboat, a utilitarian and administration assistant for Discord. It's a bot that was built to be highly configurable, and allow server admins to modify functionality based on the requirements of individual servers. The freely hosted version of Rowboat is private, and only added on high-traffic servers. HepBoat is open-source.

## Use Cases

#### Multiple Mod Logs

By using Rowboat's support for multiple mod logs, admins are able to split and categorize logs into various channels, reducing noise without sacrificing logging.

#### Spam Prevention

By turning on spam prevention, HepBoat takes a huge burden off moderators and ensures the server is safe even when nobody is watching. With the high level of configurability it is able to ensure a level of security which does not impact normal chat, but catches bad actors quickly and efficiently.

## User Testimonials

### Looney - Events and Community for Discord

> Rowboat has allowed us to efficiently scale the moderation teams of our large public and private community servers, without placing extra burden on our volunteer moderators or sacrificing auditability.

## Plugins

* Administration
  * Banning, kicking, muting
  * Managing and tracking infractions and reasons per user and moderator
  * User persistence \(resetting roles/nickname/etc when users leave and rejoin\)
  * Chat cleaning and archiving
  * Granular role management \(adding/removing roles\)
  * Invite pruning
  * Reactions pruning
  * Voice logs
* Censor
  * Zalgo prevention
  * Whitelisting of invites based on vanity url or destination server
  * Whitelisting of URLs and domains
  * Blocking of words and tokens
  * Level based configuration granularity
  * User nickname filtering
* Mod Log
  * Granular logging of events
  * Support for multiple channels
  * Ability to include exact timestamps in specific timezone
  * Ignoring and filtering of specific users \(helpful for music/etc bots\)
  * Highlighting newly created accounts on join
  * Support for automatic batching during high-throughput periods \(user purges, raids, cleans, etc\) prevents log messages from backing up
* Reddit
  * Support for multiple subreddit sources and channel destinations
  * Support for filtering nsfw content
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
  * Optional raid prevention
* Starboard
  * Highly configurable
  * In-depth stats and leaderboard
  * Ability to entirely block users from starboard
  * Ability to lock/unlock starboard on-demand
* Utilities
  * Long-term persistent reminders
  * Random number and coin generation
  * User information, including last seen time
  * Server information
  * User search
  * CAT PHOTOS
