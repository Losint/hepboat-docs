# Changelog

#### 17 Jul 2019
* Added ability to set infractions silently without dm, with forced dm, and with anonymous forced dm in the infraction plugin.
* Added ability to set delayed auto roles on join in the utility plugin.
* Added an anti-hoist nickname censor in censor plugin.
* Added ability to set kick, tempban, and ban as antiraid actions instead of only assigning a raid role in the censor plugin.
* Added 'ml' infraction identifier for "my last" infraction when using `inf reason`.
* General bug fixes.

#### 14 Jul 2019
* Added ability to set server timezone in the commands plugin to localize any timestamps in command outputs.
* Added strict channel filter configurations in the utilities plugin. e.g. set image-only or text-only channels.
* Added `notseen` command in utilities plugin.
* Users that spam the bot with DMs will now be banned from the support guild.
* `!roles` adds a `[M]` in output if the role is currently mentionable.
* Added `unmute` as an option in custom commands.
* Added `{emoji}`, `{duration}`, and `{expire_time}` tokens for custom temporary infraction notifies.
* General bug fixes.

#### 12 Jul 2019
* Added `nick change` and `nick remove` commands in admin plugin.
* Added `{duration}` and `{expire_time}` tokens for custom temporary infraction modlogs.
* General bug fixes.

#### 11 Jul 2019
* Fixed `MEMBER_ROLE_REMOVE` action name in modlog documentation.
* Added `BOT_DEBUG` action to modlog plugin to log command failure reasons.
* Added `role spray`, `role nuke`, and `role cancel` commands to admin plugin.
* Users that DM HepBoat with an invite link will now collect infractions.
* Listen-type custom commands can now be configured in lockdown in the commands plugin.
* Anti-raid notify role now properly notifies in pretty mode modlogs.
* Rewrote custom commands plugin documentation and fixed custom commands.
* Fixed `filter_invites` and `filter_domains` in censor plugin to filter everything by default if neither whitelists or blacklists are set.
* Fixed looping blocked nickname bug in censor plugin.
* General bug fixes.

#### 03 Jul 2019
* Added `mention` commands in the admin plugin.
* Added a `cleanban` command in the infractions plugin.
* `tags all` now outputs in alphabetical order. `tags list` is also an alias for the command now.
* General bug fixes.

#### 29 Jun 2019
* Added a `nuke` command for administrators in the admin plugin. 
* Change the all caps filter in the censor plugin to also count number of messages before triggering.
* Update comment links in Reddit modfeeds to use context.
* Kicks actually notify users now if enabled in infractions plugin.
* Added an `infractions clearall` command in infractions plugin.
* The `slowmode` command now defaults to minute durations and can now read human-readable durations as well and be sent remotely for another channel.
* General bug fixes.

#### 17 Jun 2019

* Added all caps filter in censor plugin. Read the doc page to learn more.

#### 15 Jun 2019

* Fixed a bug with antiraid logs
* Added ability to cleaan and/or archive reports from reddit mod feeds.
* A single multi-reddit feed is now allowed in your reddit config to get around the maximum number of a single subreddit feeds (currently 3)

#### 13 Jun 2019 

* Fixed `shut`, `unshut`, `cease`, `uncease` and `report` commands.
* Bug fixes with `Antiraid` configuration
* Custom Commands and Short Tags are now logged
* Twitch plugin fixes; it should now be fully working and announcing. 

#### 6 Jun 2019

* Custom Command bug fixes, yay!
* Added ability for mentions in tag and custom command bodies, read the respective plugin pages to learn more
* Added hepboat ban info in modlog for a user on join
* Added modlog feed option for reddit moderators

#### 1 Jun 2019

* Reddit plugin now has moderator feeds.
* Censor plugin can now censor user, role, and channel mentions.
* `exclude_category` as well as Category Create/Delete logs in Modlog Plugin.
* Cleaned up content in `!tags all`

#### 27 May 2019

* Tags can now be used in certain channels or ping users with flags. Such as !tagname !c CHANNELID !u USERID
* Twitch plugin is working again! Or actually, for the first time!
* Autolevel fixes and improvements.
* Infraction improvements and fixes.

#### 20 May 2019

* Huge feature! Now, you can now have embeds for your logs! Just enable it with modlog `mode: pretty`
* Added delay_sec to Reddit plugin to delay posting things until they are at least x seconds old, so that it doesn't post things that may get removed by a bot or even your own mods.
* Add subreddit name and time posted in footer for reddit feed posts in pretty format. 
* Bug fixes, more auto deletes have been removed, and stability improvements.
* Added more information to footer embeds for Reddit, to show the sub it's coming from, and the time it was posted.
* Fixed tags to be a little faster and not completely stop working whenever it feels like it.
* Adjusted !server info details to be more verbose.
* !info only shows 25 roles max for a user for those spicy guilds that broke the info command with 200 roles. *You know who you are*
* Blocked words censor works on message attachment names.

#### 18 May 2019

* Added more badges for roles based in our control server. Join with the link above!
* Added being able to edit tags with !tags edit name for example.
* Better logging and less deleting of helpful messages.
* Colorful embeds that were all kinda blue before.
* Informational commands.

#### 9 May 2019

* Huge amount of bug fixes and improvements
* Added some command aliases for the lazy, yours to discover!
* Added some "HepBoat is typing" indicators for commands that may run for a long time
* An entire badge system? Check your local info command today!

#### 6 Mar 2019

* `v-snap` command for mods to get list of users currently in voice chat with them. \(helpful for checking later when there's issues going on\)

#### 22 Feb 2019

* Ability to turn off twitch announcing the stream, still granting a role if one is specified to grant to those streaming.

#### 20 Feb 2019

* Twitch notification webhooks
* Twitch notification streamer name/avatar
* Twitch notification footer \(twitch logo, Live @ time\)

#### 19 Feb 2019

* Bug fixes for undefined prefixes in channel configs
* Bug fixes for nickname censor
* Control messages for reloading plugins
* Control messages for guild join/leave
* Change default logging to WARNING, command to change log level at will
* \(In progress\) Webhooks for twitch notifications

#### 17 Feb 2019

* Auto level VC issues are fixed
* Twitch plugin
  * Can set configs to strings now. This means you can have the same channel multiple times
    * Allows setting channel\_id in each config to specify the channel id
  * Fixed regex issues when specifying custom messages
  * Embeds and message now use the display name not the login name
* Discord invites in censor plugin are escaped
* Clean all and clear will no longer delete pinned messages
* Cleaned up role reactions
  * Reactions that should not be on a message will be removed \(Slowly so it doesn't hit rate limits\)
  * Specifying `join_only` or `leave_only` as an emoji list item will set that reaction to only allow the role to be joined or left but not both.
* Reworked most of the mass infraction commands. No timeouts will occur meaning you can mass ban etc quickly as expected.
* Tags with PNG and JPEG should correctly attach the picture and NOT include the URL

#### 15 Feb 2019

* Twitch plugin!! 

#### 14 Feb 2019

* Updated auto level to include guild rank, top command and the ability for global admins to import points from tatsumaki and mee6

#### 31 Jan 2019

* Reddit notify role
* Fixed some reddit plugin unescape issues
* `clean` deletes command
* Announcement config and command to send announcements to a channel
* Autoclean configuration
* Reaction based roles

#### 29 Jan 2019

* New plugin!! Autolevel that reward roles for users participation in chat!

#### 27 Jan 2019

* Antiraid! Check the censor plugin for details

#### 24 Jan 2019

* Added roles, categories to command lockdown
* Added channel and category blacklists to command lockdown

#### 20 Jan 2019

* Welcome message config - per-channel, dm or not, replacements for server/user/channel

#### 18 Jan 2019

* We're in 2019, oops, Tobiah put Jan 2018.
* Better spotify support for info command
* Duck command _cringe_
* Automatically add roles on user join with `onjoin_roles` in admin plugin

#### 14 Jan 2019

* Mobile modding, requires `mobile_mod_channel` to be configured in the admin plugin, allows initiation of mod actions via `!minfo {user id}` or reacting with 🔗 \(link emote\) on a message. The bot will walk the mod through moderation options

#### 10 Jan 2019

* `shut`/`unshut` commands to force everyone to PTT \(once discord fixes its bug, it will make no one able to speak\)
* `force setup` for a guild in cases where admins on the server cannot run it or there is an error doing it the traditional way.

#### 4 Jan 2019

* Cease/uncease \(yeet/yote\) commands to lock down channel or guild easily.
* Move archive and backup commands to admin level
* Global admin command override
* Advanced user info search
* Advanced infraction search
* Advanced user infraction lookup
* Bot status setting
* Documentation for whitelisting/unwhitelisting
* Guild Flag editing
* Mass unban/ban/mute/unmute commands
* Document some sql plugin commands
* SQL optimizations
* Frontend statistics support
* `!timeleft` to allow muted users to check remaining time

#### 18 Dec 2018

* Added control messages for dm's to the bot
* Added control message for global admin going live
* Added override command for global admins to have to use override command to enable override mode in specific servers or all. \(Sends a control message, no more than 3600s\)

#### 14 Dec 2018

* Added `dm_denied` option, allowing server owners to have the bot DM the users who attempt to use commands that are denied, or to leave it silent. \(True notifies, False does not\)
* Added `global_blacklist` and `local_blacklist`, allowing bot owner and server owners, respectively, to provide a list of users for the bot to ignore globally and per-server, respectively.

#### 10 Dec 2018

* Added  exclude\_msg\_usr to allow excluding a user from logging
* Alias for `clean all` as `clear`

#### 6 Dec 2018

* Added channel\_whitelist config option to spam filtering

#### 6 Dec 2018

* Added channel\_whitelist config option to spam filtering

#### 5 Dec 2018

* Added custom commands plugin page with detail about configuration
* Added slowmode notes to admin plugin
* Added floof command notes to utilities
* Added aliases to cat and dog commands
* Noted that when search returns a single result it will automatically turn into the info command
* Added detail to infractions regarding hard\_mute\_ignore option
* Added detail to infractions regarding temprole command

#### 3 Dec 2018

* Allow tags to have a role whitelisted wherein that role can run tags anywhere
* Allow commands to be whitelisted for a role to run it anywhere

#### 20 November 2018

* Say commands with/enabling config \(`!say channel #channel message` and `!say user @user message`\)
* Tags as first-class dynamic commands locked to admins.

#### 17 November 2018

* Role Info command \(notable perms\)
* User info enhancement \(notable perms\)
* Track role counts
* Avatar command for checking user avatar
* Increase info timeout

#### 16 November 2018

* Remove forceban, ban automatically checks it
* Restrict commands to specific channels
* Whitelist channels from incurring specific censors
* Automatically move muted user to AFK or override VC



