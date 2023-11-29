# LM Studio Discord Bot

Example Discord bot written in Python that uses the [chat completions API](https://platform.openai.com/docs/api-reference/chat/create) to have conversations with the lmstudio local model running on local server, and the comments out all the [moderations API](https://beta.openai.com/docs/api-reference/moderations) crap that filter the messages.

This bot uses the [OpenAI Python Library](https://github.com/openai/openai-python) and [discord.py](https://discordpy.readthedocs.io/).

# Features

- `/chat` starts a public thread, with a `message` argument which is the first user message passed to the bot. You can optionally also adjust the `temperature` and `max_tokens` parameters.
- The model will generate a reply for every user message in any threads started with `/chat`
- The entire thread will be passed to the model for each request, so the model will remember previous messages in the thread
- when the context limit is reached, or a max message count is reached in the thread, bot will close the thread
- you can customize the bot instructions by modifying `config.yaml`
- you can change the model, the default value is `gpt-3.5-turbo`

# Setup

1. Copy `examplenv` to `.env` and start filling in the values as detailed below
1. Copy OLDconfig.yaml to config.yaml and change it to your liking
1. Create your own Discord application at https://discord.com/developers/applications
1. Go to the Bot tab and click "Add Bot"
    - Click "Reset Token" and fill in `DISCORD_BOT_TOKEN`
    - Disable "Public Bot" unless you want your bot to be visible to everyone
    - Enable "Message Content Intent" under "Privileged Gateway Intents"
1. Go to the OAuth2 tab, copy your "Client ID", and fill in `DISCORD_CLIENT_ID`
1. Copy the ID the server you want to allow your bot to be used in by right clicking the server icon and clicking "Copy ID". Fill in `ALLOWED_SERVER_IDS`. If you want to allow multiple servers, separate the IDs by "," like `server_id_1,server_id_2`
1. Install dependencies and run the bot
    ```
    pip install -r requirements.txt
    python -m src.main
    ```
    You should see an invite URL in the console. Copy and paste it into your browser to add the bot to your server.
    Note: make sure you are using Python 3.9+ (check with python --version)
    Note: you only need to do the invite link once

# Optional configuration

1. If you want to change the personality of the bot, go to `src/config.yaml` and edit the instructions

# FAQ

> Why isn't my bot responding to commands?

Ensure that the channels your bots have access to allow the bot to have these permissions.
- Send Messages
- Send Messages in Threads
- Create Public Threads
- Manage Messages (only for moderation to delete blocked messages)
- Manage Threads
- Read Message History
- Use Application Commands
