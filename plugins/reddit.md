# Reddit Plugin

The Reddit plugin provides a feed of new posts on specified subreddits.

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| subs | A mapping of subreddits to Subreddit Configurations | dict | empty |

### Subreddit Configuration

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| channel | Sets which channel the feed should post subreddit threads to | dict | empty |
| mode | Format of the entries. Options: `PRETTY, PLAIN` | str | pretty |
| nsfw | Whether to include NSFW posts | bool | false |
| include\_stats | Whether to include stats for each thread | bool | false |
| notify\_role | Role to notify of posts to this subreddit | snowflake | empty |
| delay_sec: | Number of seconds to delay the post feed | int in seconds | 0

## Configuration Example

```yaml
  reddit:
    subs:
      discordapp:
        channel: 281855195095236608
        mode: pretty
        nsfw: false
        delay_sec: 120
        include_stats: true
        notify_role: 148516565858385920
```
