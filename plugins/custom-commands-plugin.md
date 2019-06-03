# Custom Commands Plugin

The custom commands plugin allows guild admins a way to create custom commands that allow multiple actions to be performed when the required trigger is done. This can be defined as an in chat command or by waiting for specific actions to occur such as a message containing a specific string.  
  
The difference between a custom command and a tag is essentially a tag is just a text response to a command being run. This could be used to hold some useful information for a channel for instance. A custom command however while is can similar to a tag can chain multiple actions together such as adding/removing roles and other actions such as bans/kicks/warnings all in a single chained set of actions.

All commands in custom commands are configured to ADMIN \(level 100\) due to how sensitive the commands can be. Incorrectly creating commands **can** allow privileged access where it was not intended. There is no permissions checking when creating or running any of these commands. An example of this is if you create a command that grants admin access in some way it will grant admin access to ANYONE who is able to trigger this by default. The hardening section shows a recommended configuration that will lock down created custom commands to a specific admin channel so they can be individually leaked into user channels.

## Commands

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Usage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>!cc all</code>
      </td>
      <td style="text-align:left">Displays all defined custom commands</td>
      <td style="text-align:left"><code>!cc all</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>!cc info {name}</code>
      </td>
      <td style="text-align:left">Display information about the named custom command</td>
      <td style="text-align:left"><code>!cc info kittens</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><code>!cc delete {name}</code>
        </p>
        <p><code>!cc del {name}</code>
        </p>
        <p><code>!cc rm {name}</code>
        </p>
      </td>
      <td style="text-align:left">Deletes the named custom command</td>
      <td style="text-align:left">
        <p><code>!cc delete kittens</code>
        </p>
        <p>OR</p>
        <p><code>!cc del kittens</code>
        </p>
        <p>OR</p>
        <p><code>!cc rm kittens</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>!cc create {name} {type} {listen_type} &lt;command1&gt; | &lt;command2&gt;</code>
      </td>
      <td style="text-align:left">Creates a custom command with defined attributes as detailed below</td>
      <td
      style="text-align:left"><code>!cc create testing cmd 0 notify | addgroup cats | addgrouptemp dogs 20m</code>
        </td>
    </tr>
  </tbody>
</table>

## Command Options

### Type

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Info</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">cmd</td>
      <td style="text-align:left">
        <p>cmd defines a command that is run by running the command name in a channel</p>
        <p>E.g. <code>!showmecats</code> which will execute the commands contained
          within the showmecats command</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">listen</td>
      <td style="text-align:left">
        <p>listen uses the disco defined listen handlers to perform actions automatically
          when the {listen_type} and its triggers are executed</p>
        <p>E.g. <code>!cc create listen MessageCreate reply cats I like cats to</code>
        </p>
        <p>When this command detects the string cats it will reply with <code>I like cats to</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>
 
### Listen Type

| Name | Info |
| :--- | :--- |
| MessageCreate | Command is triggered when a message is created and a specific defined action is performed |
| 0 | If the type is `cmd` anything can be defined for the Listen Type such as 0 |

### cmd commands

<table>
  <thead>
    <tr>
      <th style="text-align:left">Command</th>
      <th style="text-align:left">Info</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">allowargs</td>
      <td style="text-align:left">
        <p>Should be defined first if possible. This allows the command to accept
          arguments to override the user and reasons</p>
        <p>E.g. <code>!custcmd &lt;user&gt; [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">notify</td>
      <td style="text-align:left">Should be defined first if possible. This will enable notifications for
        every command that executes after the notify command</td>
    </tr>
    <tr>
      <td style="text-align:left">addgroup
        <rolename>
      </td>
      <td style="text-align:left">
        <p>Will add a role to the user running the command</p>
        <p>E.g. <code>addgroup &lt;rolename&gt;</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">removegroup
        <rolename>
      </td>
      <td style="text-align:left">
        <p>Will remove a role from the user running the command</p>
        <p>E.g. <code>removegroup &lt;rolename&gt;</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">addgrouptemp
        <rolename>
          <duration>[reason]</td>
      <td style="text-align:left">
        <p>Will add a temp role to the user for the defined duration</p>
        <p>E.g. <code>addgrouptemp &lt;rolename&gt; &lt;duration&gt; [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">kick [reason]</td>
      <td style="text-align:left">
        <p>Will kick the user from the guild</p>
        <p>E.g <code>kick [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">tempban
        <duration>[reason]</td>
      <td style="text-align:left">
        <p>Will temp ban the user for the defined duration</p>
        <p>E.g <code>tempban &lt;duration&gt; [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">softban [reason]</td>
      <td style="text-align:left">
        <p>Will ban and immediately unban the user from the guild</p>
        <p>E.g <code>softban [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ban [reason]</td>
      <td style="text-align:left">
        <p>Will ban the user from the guild</p>
        <p>E.g. <code>ban [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">warn [reason]</td>
      <td style="text-align:left">
        <p>Will warn the user</p>
        <p>E.g. <code>warn [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">mute [reason]</td>
      <td style="text-align:left">
        <p>Will mute the user</p>
        <p>E.g. <code>mute [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">mutehard [reason]</td>
      <td style="text-align:left">
        <p>Will hard mute the user</p>
        <p>E.g. <code>mutehard [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">tempmute
        <duration>[reason]</td>
      <td style="text-align:left">
        <p>Will mute the user for the defined duration</p>
        <p>E.g. <code>tempmute &lt;duration&gt; [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">tempmutehard
        <duration>[reason]</td>
      <td style="text-align:left">
        <p>Will hard mute the user for the defined duration</p>
        <p>E.g. <code>tempmutehard &lt;duration&gt; [reason]</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">mutevc</td>
      <td style="text-align:left">
        <p>Will move the user to the defined AFK voice channel</p>
        <p>E.g. <code>mutevc</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>

### Listen Commands

#### MessageCreate

| Command | Info |
| :--- | :--- |
| reactall &lt;channelid&gt; &lt;emoji\_id&gt; | Will react to everything in the defined channel with the emoji. The emoji\_id must include the name such as `smile:501155013431787530` |
| replyall &lt;channelid&gt; \[reply\] | Will reply to everything in the defined channel with the reply message. |
| react &lt;searchstr&gt; &lt;emoji\_id&gt; | Will react to all instances of &lt;searchstr&gt; with the emoji. The emoji\_id must include the name such as `smile:501155013431787530` . &lt;searchstr&gt; can include multiple words, if surrounded by quotes e.g. `haha xd` is a valid str. |
| reply &lt;searchstr&gt; \[reply\] | Will reply to all instances of &lt;searchstr&gt; with the reply message. |
| replycmd `cmd search str` `msg` | Will reply to all instances of !cmd with the reply message. e.g. `!!cc create cmd_tagsowo_reply listen MessageCreate replycmd 'tags owo' :rabbit:` |
| reactcmd `cmd search str` `emoji` | Will react to all instances of !cmd with the react emoji |

## Configuration Options

Guild level configuration to enable the custom commands feature within the guild:

```yaml
plugins:
  custcommands: {}
```

## Hardening

The following configuration is a recommended guild level configuration to apply to harden the custom commands feature:

```yaml
commands:
  overrides:
  - name: cc-usr
    out:
      level: 100
  lockdown:
  - group: cc
    out:
      channels: [504782681263964162] # Admin commands channel
  - name: cc-usr
    out:
      channels: [504782681263964162] # Admin commands channel
```

### Guild Hardening Options

The configuration for this plugin uses the commands plugin within the core of the bot to apply overrides and lockdowns to both command levels and channel lockdowns.

cc-usr is applied to all created custom commands. It is recommended to set this to the following configuration as otherwise by default ANY custom command that has been created can be run by any user as the default level is 0
commands:

```yaml      
overrides:
  - name: cc-usr
    out:
      level: 100
```      

This should also be channel locked as a recommendation:
commands:

```yaml
lockdown
  - name: cc-usr
    out:
      channels: [504782681263964162] # Admin commands channel
```
When you have created a custom command you should use similar config as shown above in cc-usr example with a level of 0 or the required level including lockdown configuration        

When a command is created it will automatically be locked to level 100 permissions and within the admin channel only. From here if required you can leak the individual commands out as follows.  
E.g. of command called showjokes

```yaml
commands:
  overrides:
  - name: cc-usr
    out:
      level: 100
  - name: showjokes
    out:
      level: 0
  lockdown:
  - group: cc
    out:
      channels: [504782681263964162] # Admin commands channel
  - name: cc-usr
    out:
      channels: [504782681263964162] # Admin commands channel
  - name: showjokes
    out:
      channels: [504782681263964123] # User commands channel
```