# Reddit Plugin

Plugin name: `reddit`

The Reddit plugin provides a few various Reddit feeds including new posts on specified subreddits and different types of private moderation feeds.

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| subs | A mapping of subreddit names to subreddit configurations. | dict | empty |
| mod_feeds | A mapping of usernames to mod feed configs. | dict | empty |
| multi | A single multireddit config. | dict | empty |

### Subreddit Configuration

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| channel | Channel to send feed messages.  | snowflake | empty |
| mode | Type of feed message. Options: `PLAIN`, `PRETTY`. Pretty mode uses embedded messages. | str | `PRETTY` |
| nsfw | Whether to include NSFW posts. | bool | false |
| include_stats | Whether to include upvote/downvote data and comment stats on each post. | bool | false |
| notify_role | Role to notify on each new post. | snowflake | empty |
| delay_sec | Seconds to delay the post feed. | int | 0 | 

### Mod Feed Configuration 

| Option | Description | Type | Default
| :--- | :--- | :--- | :--- | 
| mod_hash | The username's private feed hash key. See instructions below. | str | empty | 
| channels |  A mapping of channels to mod feed channel configs. | dict | empty | 
| channels -> `enable_mod_listings:` | A list of private moderation feeds to enable. Options: `SPAM`, `REPORTS`, `NEW_MODMAIL`, `MODLOG` | list(str) | empty
| enable_clean | Enables option to delete or archive reports. | bool | false 
| archive_channel | Archive channel for reports. | snowflake | empty

If `enable_clean` is true, a clipboard reaction is added to every report. Reacting to the clipboard will add a checkmark and an x reaction. The timeout to react to the additional reactions is 30sec.

If the checkmark reaction is selected, the report will be deleted if `archive_channel` is false and archived into the `archive_channel` if true.

If the x reaction is selected, the checkmark and x will be removed and only the clipboard will remain.

#### `mod_hash` Setup

If you are a moderator in any subreddit:

1. Visit https://old.reddit.com/prefs/ and make sure that `enable private RSS feeds (available from the 'RSS feed' tab in prefs)` is checked.
1. Visit https://old.reddit.com/prefs/feeds/.
1. Open any of the RSS or JSON feeds and look at the URL which should look similar to `https://old.reddit.com/user/redditor/downvoted.rss?feed=12327266948a123979d1114afd8b123d542be9cd&user=redditor`.
1. The mod_hash to copy is after the `feed` parameter. In the above example, you would want to copy `12327266948a123979d1114afd8b123d542be9cd` to your config.

### Multireddit Configuration
A [multireddit](https://www.reddit.com/r/announcements/comments/bpfyx1/introducing_custom_feeds_plus_a_community_contest/) is a user-created Reddit custom feed that can contain a multitude of subreddits. This allows users to overcome the limitation of the maximum of three single subreddit feed configurations. However the multireddit feed may only be posted in one channel.

| Option | Description | Type | Default
| :--- | :--- | :--- | :--- | 
| username | Username that created the multifeed. | str | empty |
| feed_name | The custom feed name. | str | empty |
| channel | Channel to send feed messages.  | snowflake | empty |
| mode | Type of feed message. Options: `PLAIN`, `PRETTY`. Pretty mode uses embedded messages. | str | `PRETTY` |
| nsfw | Whether to include NSFW posts. | bool | false |
| include_stats | Whether to include upvote/downvote data and comment stats on each post. | bool | false |
| notify_role | Role to notify on each new post. | snowflake | empty |
| delay_sec | Seconds to delay the post feed. | int | 0 | 

For an example multireddit feed with the URL `https://www.reddit.com/user/redditor/m/rabbits/`, the `username` would be `redditor` and the `feed_name` would be `rabbits`.

## Configuration Example

```yaml
plugin:
  reddit:
    subs:
      aww: # Subreddit name
        channel: 579533838892400659
        mode: pretty
        delay_sec: 10
    mod_feeds:
      alchameth: # Reddit Username
        mod_hash: 75efda66948a68c979d11254afd1b621c542be9cf
        channels:
          583887495733968909:
            enable_mod_listings:
              - REPORTS
              - SPAM
              - NEW_MODMAIL
              - MODLOG
        enable_clean: true
        archive_channel: 583887225733968463
    multi:
      username: alchameth
      feed_name: rabbits
      channel: 433763867808122625
      delay_sec: 300
```