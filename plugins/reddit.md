# Reddit Plugin

The Reddit plugin provides a feed of new posts on specified subreddits.

## Configuration Options

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| subs | A mapping of subreddits to Subreddit Configurations | dict | empty |
| mod_feeds | A mapping of usernames to mod feed configs | dict | empty |

### Subreddit Configuration

| Option | Description | Type | Default |
| :--- | :--- | :--- | :--- |
| channel | Single channel the feed should write posts to | snowflake | empty |
| mode | Format of the entries. Options: `PRETTY, PLAIN` | str | pretty |
| nsfw | Whether to include NSFW posts | bool | false |
| include\_stats | Whether to include upvote/downvote and comment stats on each post | bool | false |
| notify\_role | Role to notify on each new post | snowflake | empty |
| delay_sec: | Number of seconds to delay the post feed | int in seconds | 0 | 

### Mod Feeds Configuration 

| Option | Description | Type | Default
| :--- | :--- | :--- | :--- | 
| channels | mapping of channels to mod feed channel configs | dict | empty | 
| mod_hash | The username's private feed hash key. See instructions below.  | str | empty | 
| channels -> `enable_mod_listings:` | list of feeds to enable in the channel. Options: `SPAM`, `REPORTS`, `NEW_MODMAIL` | list(str) | empty

### Mod_hash Setup

If you are a moderator in any subreddit:

- Head over to [THIS LINK](https://www.reddit.com/r/mod/about/modqueue/.json?feed=HASH&user=REDDIT_USERNAME) 
- (change the reddit_username in the URL)
- copy the `{"modhash": "82efda66948a68c979d1114afd8b621f542be9cf"}` key; This is to be used in the `mod_hash` subconfig option, as shown below.

## Configuration Example

```yaml
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
```
