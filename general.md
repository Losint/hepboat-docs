# General Configuration

This page covers the main level basic configuration options.

## Web

```yaml
# Sample web configuration
web:
  80351110224278912: admin  # b1nzy
  108598213681923048: editor  # JakeyPrime
  84912325282254848: viewer # Alchameth
  189990173222164545: viewer  # Bunnerz
```

Web determines which users are able to view the configuration dashboard for the server. Commenting a line with the username next each user ID helps with organization.

User ID is used to assign ranks. There are three ranks you can assign: admin, editor, viewer. `Admin` can add more users (including other Admins), edit, and view the dashboard. `Editor` can edit and view the dashboard. `Viewer` can only view the configuration.

Adding users to your config will grant them the "Verified HepBoat User" role in our support guild, which they can join by clicking the `Support Server` link at the top of the page. This will give them access to a Discord server where they can talk with other HepBoat users and get support from our amazing HepBoat support team.

## Nickname

```yaml
# Sample nickname configuration
nickname: H3PB0AT
```

Set a nickname for the bot! Nickname is automatically applied upon the global reload of the bot. You may also give the bot a custom nickname in the server directly in the meantime.

## Levels

```yaml
# Sample level configuration
levels:
  290295854124550657: 100 #Admin
  295472842935353345: 50 #Moderator
  298993418577703616: 10 #Trusted
```
This is where you assign levels to each role in your server! Remember, the default level is 0 if a user does not have one of the explicitly listed roles. Users will have the highest level of their assigned roles.

By default, some levels have a certain rank associated with it: 
```
0 - Default
10 - Trusted
50 - Mod
100 - Admin
```

You can view the default rank required for each command by looking at the Commands section for each plugin.

Levels can be set to any positive integer. Keep in mind the default permissions given for each command. You can override the default ranks for commands by using the command configuration explained below.

## Commands and Overrides

Check out the [Commands plugin](plugins/commands-plugin.md) page for full documentation.

```yaml
# Sample commands configuration
commands:
  prefix: '!'
  overrides:
  - plugin.name: 'utilities', out: {level: 10}
  - group: clean
    out: 
      level: 40
  - name: mute
    out:
      level: 40
```
Here, you can change your prefix, which is the string of characters which will trigger each command.
```yaml
# Some prefix examples
prefix: '!'   # !ban
prefix: '!!'  # !!ban
prefix: '$'   # $ban
prefix: '^'   # ^ban
prefix: 'rb!' # rb!ban
```

Overrides allow you to customize which levels and roles can use each command, or group of commands.
* `plugin.name` is used for all commands in a plugin (Hint: every section that's indented one in beneath the "plugins:" 
section is a plugin)
* `group` is used for commands which have multiple components. Some examples: `clean`, `archive`, `role`, `stars`
* `name` is used for specific commands.
* `out: {level: 40}` is used to assign the minimum level required to use the command.

Taking the configuration above as an example, the given server would have the following features:
* Regular users with a default level of 0 would be unable to use utility commands (such as `jumbo`, `info`, and `cat`).
* The `clean` command group had a default level of 50 (moderator) to use the commands, but now users will only need a 
minimum level of 40 to use them.
* The `mute` command had a default level of 50 (moderator) to use the commands, but now users will only need a 
minimum level of 40 to use them.


