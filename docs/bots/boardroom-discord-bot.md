---
description: >-
  A DAO Bot that easily lets you track and subscribe to governance activity in
  your Discord server
---

# 💬 Discord Bot

This is a bot that interacts with [Boardroom's API](../boardroom-api/boardroom-api/) and allows communities to track active proposals by displaying them within a discord server.

## Setup

_The bot is configurable for individual DAOs._&#x20;

<!-- theme: info -->

> Start by [**cloning this code from GitHub**](https://github.com/boardroom-inc/boardroom-bot-discord) to your own computer or server.

1. Create a new file in the base directory named `.env`
2. Copy the `BOT_TOKEN` and `DAO` lines from the `sample.env` file and put them into the `.env` file.
3. Set the DAO variable to be the name of the DAO that you wish to use from the Boardroom URL
   1. For example, Shapeshift would use 'shapeshift' since that is what is in the URL here: "[https://boardroom.io/shapeshift/overview](https://boardroom.io/shapeshift/overview)"
4. Set the `BOT_TOKEN` to your Discord's bot token
   1. The setup for that can be found [here](https://discordpy.readthedocs.io/en/stable/discord.html)
   2. Make sure to invite the bot to your Discord
5. Finally, run `node index.js` to start the bot.&#x20;

<!-- theme: success -->

> Now you can type `!proposals` in your Discord Server to see active proposals for your DAO!

---

_If you want to run the bot on a server, forever.js can be used to set up the bot to continuously run:_  [_https://www.npmjs.com/package/forever_](https://www.npmjs.com/package/forever)
