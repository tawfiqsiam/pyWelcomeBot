# pyWelcomeBot
Simple Discord bot written in Python to welcome new members to a Discord server and alert admins when members leave the server.

# Introduction
The bot was originally intended to welcome new members to a Discord server upon joining and alert server admins when members departed the server. The original functionality within the bot remains, however, it has evolved into a hodge podge of tools (mostly administrative) that will be explained in further detail.

The bot functionality is split into three groups: monitoring functions, background tasks, and commands. The first group represents functions that are invisible to the user and execute any time a message is posted to the server (excluding private messages). The second represents background tasks that execute based on a prescribed schedule. The last represents commands that can be invoked as needed from within Discord.

# Dependencies

# Monitoring Functions
### New and Departed Members
The bot welcomes users to the Discord server and alerts admins of any members who have departed. The contents of the message for new and departed members, along with specific channels to which the message is sent, is stored within the bot configuration file.

### Collection of Message Metadata
Under development: The bot collects metadata for all messages posted to the server excluding private messages, messages within certain channels, and messages from certain users. The message metadata is sent directly to an Amazon SQS (Simple Queue Service) message queue. The message queue triggers a serverless AWS Lambda function which parses the metadata and stores the data in a PostgreSQL database for analytics.

# Background Task(s)
### Online Clan Members
Added a background task to the bot that builds a list of clan members in-game every two minutes. The list is written to a Redis cache in order to support faster retrieval from the bot.

An example of the formatted list stored in the cache:

```
{
  "Iron Orange Earth": "mr_rots: Social - Tower (0.00m)\nRetired_Lenni: Explore - Hellas Basin (15.17m)",
  "Iron Orange Mars": "SheNanigans_85_: Explore - Titan (19.14m)"
}
```

Added an **on_message** event to listen for the command *!online*. The command calls an API endpoint that retrieves a list of clan members in-game and sends a direct message to the user who invoked the command.

### Daily Pull of Discord Accounts

# Supported Commands
## !online - TODO: Add details
## !link report - TODO: Add details
## !link gamertag:gamertag discord:discord - TODO: Add details




