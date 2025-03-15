## Updates

Welcome to our NFD2.0 project 🎉, quick setup guide in 1 minute:

> First, users go to [@BotFather](https://t.me/NodeForwardBot/BotFather), enter `/newbot`, follow the prompts to enter the nickname and name of the bot you want to create, and click to copy the token provided by the bot
> 
> Then go to [@NodeForwardBot](https://t.me/NodeForwardBot) and paste it. That's it.
> 
> For detailed information, please refer to: [https://www.nodeseek.com/post-286885-1](https://www.nodeseek.com/post-286885-1)

NFD2.0 has unlimited quota (self-hosted has a daily limit of 1k messages), and is hosted on [cloudflare snippets](https://developers.cloudflare.com/rules/snippets/), theoretically it will not go offline. If you need to self-host, refer to the self-hosting tutorial below.

# NFD
No Fraud / Node Forward Bot

A Telegram message forwarding bot based on Cloudflare Worker, integrated with anti-fraud functionality

## Features
- Built on Cloudflare Worker, achieving the following effects:
    - Low setup cost, only one JS file is needed to complete the setup
    - No additional domain name required, using the built-in Worker domain
    - Permanent data storage implemented based on Worker KV
    - Stable, global CDN forwarding
- Connected to an anti-fraud system, automatically sends alerts when the chat partner has a history of fraud
- Supports blocking users to avoid harassment

## Setup Method
1. Get a token from [@BotFather](https://t.me/BotFather), and you can send `/setjoingroups` to prevent this Bot from being added to groups
2. Get a random UUID from [uuidgenerator](https://www.uuidgenerator.net/) as a secret
3. Get your user ID from [@username_to_id_bot](https://t.me/username_to_id_bot)
4. Log in to [Cloudflare](https://workers.cloudflare.com/) and create a worker
5. Configure worker variables:
    - Add an `ENV_BOT_TOKEN` variable, with the value being the token obtained from step 1
    - Add an `ENV_BOT_SECRET` variable, with the value being the secret obtained from step 2
    - Add an `ENV_ADMIN_UID` variable, with the value being the user ID obtained from step 3
6. Bind a KV database, create a KV database with Namespace Name as `nfd`, in setting -> variable set `KV Namespace Bindings`: nfd -> nfd
7. Click `Quick Edit`, copy [this file](./worker.js) to the editor
8. Register the websocket by opening `https://xxx.workers.dev/registerWebhook`

## Usage Instructions
- When other users send messages to the bot, they will be forwarded to the bot creator
- When the user replies with normal text to a forwarded message, it will be sent back to the original message sender
- When the user replies with commands like `/block`, `/unblock`, `/checkblock`, these commands will be executed and will **NOT** be sent to the original message sender

## Fraud Data Source
- The file [fraud.db](./fraud.db) contains fraud data, with one UID per line
- You can extend this data through pull requests, or supplement it by submitting issues
- When providing additional fraud information, you need to provide some message sources

## Thanks
- [telegram-bot-cloudflare](https://github.com/cvzi/telegram-bot-cloudflare)
