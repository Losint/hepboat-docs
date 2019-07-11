# Setting Up HepBoat

## Adding the Bot

HepBoat is only available to servers that meet certain criteria:

* The server does not promote or promulgate NSFW content
* HepBoat will be used to moderate, not "just for fun". We may provide one additional whitelist to a test server.
* Servers who accept that our team will only provide support for bot issues, not with setting the bot up. If you need assistance, join the support server listed above.

## How to Set Up

Firstly, you will need to be on the whitelist, there is a link above that lets you send me a message to get you added. If you invite the bot, and you aren't on the whitelist, it will immediately leave.

Once the bot is in your server, go into a chat the bot has access to, and do `@hepboat setup` it should reply with a pass and fail message, ignore this, you're good to go!
Then, go to [https://mod.teamhydra.dev//](https://mod.teamhydra.dev/) to edit your server's configuration. Use the sidebar to read about each plugin, then use the example below along with the information in the sidebar to set up your own customized HepBoat configuration.
The bot will not do anything out of the box, you'll have to continue below to enable and disable which parts of the bot you want, as you can see, it's completely modular. 

Below is a blank configuration example with web, utilities, admin, infractions, modlog, spam, and censor set up. While you can simply copy-paste this to your own server's configuration and fill in the blanks to have a perfectly usable rowboat, it's highly encouraged that you read through the full documentation to understand each component and customize rowboat to your server's needs.

## Example HepBoat Configurations

### Skeleton Configuration

```yaml
web:
  148359099782791168: admin # JakeyPrime - Change This
​
levels:
  148359099782791168: 100 # Your role id or individual admin ID's

commands:
  prefix: '!'
​
plugins:
  utilities: {}
```

### Minimal Configurations

```yaml
web:
  148359099782791168: admin      # JakeyPrime - Change This

commands:
  prefix: '!'
  overrides: # Custom commands hardening. See custom commands plugin page for more details.
  - group: cc
    out:
      roles:
        - 00000000000000000  # Admin
  - name: cc-usr
    out:
      roles:
        - 00000000000000000  # Admin        
  lockdown: 
  - group: cc
    out:
      channels: [000000000000000000]        # Admin commands channel

levels:
  180768265633660928: 100   # Server Admin Role Id
  131682843326808064: 99    # server admin bot Role Id
  274266640403791873: 60    # Senior Moderator Role Id
  77190254141911040: 50     # Moderator Role Id
  335114792820015106: 10    # Bot Role Id

nickname: H4PB0AT

plugins:
  admin:
    persist:
      roles: true
      role_ids:  # Roles to recover after leaving and joining back 
      - 000000000000000000      #  Muted Role
      nickname: true
      voice: true
        Your server log
  infractions:
    confirm_actions: true
    confirm_actions_reaction: true
    mute_role: 000000000000000000       # Muted Role
    hard_mute_role: 000000000000000000       # Muted Role
    reason_edit_level: 100
    report_channel: 535051955639418890 # Channel for reports to go to 
    notify:
      WARN:
        format: true
      BAN:
        format: true
      TEMPMUTE:
        format: true
      MUTE:
        format: true
      TEMPBAN:
         format: true
    
  modlog:
    channels:
      171383278048247808: # Server Log Channel
        exclude: []
        mode: pretty

  utilities: {}
  tags: {}
```

### Standard Basic Configuration

```yaml
web: 
  148359099782791168: admin    # JakeyPrime # Change this
  84912325282254848: editor    # Alchameth  # Change this

commands:
  prefix: '!'
  overrides: # Custom commands hardening. See custom commands plugin page for more details.
  - group: cc
    out:
      roles:
        - 00000000000000000  # Admin
  - name: cc-usr
    out:
      roles:
        - 00000000000000000  # Admin        
  lockdown: 
  - group: cc
    out:
      channels: [000000000000000000]        # Admin commands channel
      
nickname: 'HepBoat'

levels:
  000000000000000000: 100       # Admin ID
  000000000000000000: 99        # Server admin bot role ID
  000000000000000000: 60        # Senior Moderator role ID
  000000000000000000: 50        # Moderator role ID
  000000000000000000: 46        # AI - Bots roles ID
  000000000000000000: 10        # Trusted role ID
  000000000000000000: 0         # Everyone ID
 
plugins: 
  utilities: {}
  
  admin:
    persist:
      roles: true
      role_ids:  # Roles to recover after leaving and joining back 
      - 000000000000000000      #  Muted Role
      nickname: true
      voice: true
  
  censor: # You're advised to add malicious websites under domain blacklist and racial slurs and offensive words under words & token filtering
    levels:
      45:
        filter_zalgo: true
        filter_invites: true
        invites_whitelist: []
        invites_blacklist: []
        filter_domains: true
        domains_whitelist: ['000000']  # Add gibberish to filter all domains by default
        blocked_tokens: [] 
        blocked_words: []
        blocked_nicknames: []
        block_zalgo_nicknames: true

  spam:
    levels:
      45:
        punishment: TEMPMUTE # Change that if you wish : "TEMPMUTE, MUTE, KICK, BAN"
        punishment_duration: 300
        clean: true
        clean_count: 50
        clean_duration: 500
        channel_whitelist: [] # If you want to whitelist channels for anti-spam to not apply. You can also whitelist PER ANTI SPAM TYPE by adding "channel_whitelist: [ID] in the same column as count/interval.
        max_messages:
          count: 10
          interval: 7
        max_mentions:
          count: 8
          interval: 30
        max_links:
          count: 10
          interval: 60
        max_emojis:
          count: 100
          interval: 120
        max_newlines:
          count: 60
          interval: 120
        max_duplicates:
          count: 5
          interval: 30

  infractions:
    confirm_actions: true
    confirm_actions_reaction: true
    mute_role: 000000000000000000       # Muted Role
    hard_mute_role: 000000000000000000       # Muted Role
    reason_edit_level: 100
    report_channel: 535051955639418890 # Channel for reports to go to    
    notify: # 
      WARN:
        emoji: warning
        format: |-
          You have been **{action!s}** in **{guild.name}** by **{actor!s}** for `{reason!s}`.
      TEMPMUTE:
        emoji: no_mouth
        format: |-
          You have been **{action!s}** in **{guild.name}** by **{actor!s}** for `{reason!s}` until **{expires}** GMT+0.
      MUTE:
        emoji: no_mouth
        format: |-
          You have been **{action!s}** in **{guild.name}** by **{actor!s}** for `{reason!s}`.
      TEMPBAN:
        emoji: tools
        format: |-
          You have been **{action!s}** until **{expires} GMT+0 in **{guild.name}** by **{actor!s}** for `{reason!s}`.
      BAN:
        emoji: tools
        format: |-
          You have been **{action!s}** in **{guild.name}** by **{actor!s}** for `{reason!s}` .
      KICK:
        emoji: boot
        format: |-
          You have been **{action!s}** in **{guild.name}** by **{actor!s}** for `{reason!s}`. 
 
modlog: # See modlog plugin documentation for more actions to explicitly include.
    channels:
      000000000000000000:     # Message Logs
        exclude: []
        include: 
          - MESSAGE_DELETE
          - MESSAGE_DELETE_BULK
          - MESSAGE_EDIT
          - CENSORED
        timestamps: true
        timezone: GMT+0
      000000000000000000:     # Server Logs
        exclude: 
          - MESSAGE_DELETE
          - MESSAGE_DELETE_BULK
          - MESSAGE_EDIT
        include: []
        timestamps: true
        timezone: GMT+0        
      000000000000000000:     # User-Logs
        exclude: []
        include: 
          - GUILD_MEMBER_ADD
          - GUILD_MEMBER_REMOVE
        timestamps: true
        timezone: GMT+0
      000000000000000000:     # Action-Log - Your public moderation log where the server can see actions taken.
        exclude: []
        include: 
          - MEMBER_KICK
          - GUILD_BAN_ADD
          - GUILD_BAN_REMOVE
          - MEMBER_TEMPBAN
          - MEMBER_SOFTBAN
          - MEMBER_BAN
          - MEMBER_MUTED
          - MEMBER_TEMP_MUTED
          - MEMBER_WARNED          
    ignored_users: []
    new_member_threshold: 86400 # time in seconds
  
  tags:
    max_tag_length: 1000 # Set it as long as you want or remove
    min_level_remove_others: 50 # To allow only level 50 and above to remove (in this config, moderators)   
```