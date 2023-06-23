# basic-commands-python-discord-cog
This is a cog which is made for a python discord bot which runs on one server only.
It contains the following commands which are used as examples so that others can make their own cog. It supports slash 
commands.
### The commands are:
- `/ping`: sends an ephemeral message to the user containing the message `"pong"`
- `/meme`: sends a random meme using `meme-api.com`, the meme is sent as an embed and the message is deleted after 60
seconds
- `/pfp`: sends the profile picture of the requested user, if no user is requested, it sends the profile picture of the
user who requested the command. The profile picture is sent as an embed and the message is deleted after 60 seconds
### .env file:
The cog uses a .env file found in the `bot` directory. The .env file contains the following variables:
```dotenv
# standard enviroment variables
DISCORD_TOKEN=your_token
DISCORD_PREFIX=your_prefix
OWNER_ID=your_id
GUILD_ID=your_guild_id
BOT_CHANNEL_ID=your_bot_channel_id
# enviroment variables for basicCommands cog
MEME_CHANNEL_ID=your_meme_channel_id
BLACKLISTED_USERS=[id_1,id_2,id_3]
```
The standard environment variables are variables which are found in the `.env` file of the `python-discord-bot`
repository. The environment variables for the `basicCommands` cog are variables which are used by the cog. This file is
not present in the repository, so it is required to be created. The variables that are part of this cog are:
- `MEME_CHANNEL_ID`: the id of the channel where the memes will be sent
- `BLACKLISTED_USERS`: a list of user ids which are blacklisted from using the cog
### The intended design of the cog:
The cog is intended to be used with my `python-discord-bot` repository. The cog is intended to be used as a git
submodule in the `cogs_submodules` directory. The cog is intended to be used with the following directory structure:
```
basic-commands-python-discord-cog
├── bot
│   ├── cogs
│   │   └── basicCommands
│   │       └── Cog.py
│   └── .env
├── data.toml
├── docker-compose.yml
├── paths.toml
├── README.md
└── requirements.txt
```
- `bot/cogs/basicCommands/Cog.py` is the file containing the cog, the tree structure is made to replicate the structure
the tree structure of `python-discord-bot`, this is done mostly because of the usage of the `.env` which is in the same
directory as the `bot.py` file, which is the file which is run to start the bot. by replicating the structure, the
`.env` file can more easily be programmatically used.
- `bot/.env` is the environment file for the bot. Other variables can be added, these will be transferred to the `.env`
file in the root of the repository. If the variable is already in the `.env` file in the root of the repository, it will
be overwritten. You can expect the following variables to be standard with the bot:
  - `DISCORD_TOKEN`: the token of the bot
  - `DISCORD_PREFIX`: the prefix of the bot
  - `GUILD_ID`: the id of the guild the bot will be used on
  - `OWNER_ID`: the id of the owner of the bot
  - `BOT_CHANNEL_ID`: the id of the channel where the bot will be used
- `data.toml` is a file which lists the paths to the files which are used as data files. this file is to inform the
update script which files to save when updating the bot. you can expect the format of the file to be as follows:
    ```toml
    [basicCommands]
    paths = ["bot/cogs/basicCommands/example_path.json"]
    ```
  where there `basicCommands` is the name of the cog and `paths` is a list of paths to the data files.
- `docker-compose.yml` is the docker-compose file which is used to run the bot. It is an optional file in the submodule,
it can be used to add additional services to the bot, such as a database. The file will be merged with the one in the
root of the repository. You can expect the following services to be standard with the bot:
  - `bot`: the bot service, this is the service which runs the bot
- `paths.toml` is a file used by the setup script to inform the setup script which files to copy to the root of the
repository. you can expect the format of the file to be as follows:
    ```toml
    paths = ["bot/cogs/basicCommands/example_path.json"]
    ```
  where there `basicCommands` is the name of the cog and `paths` is a list of paths to the files.
- `README.md` is this file, it contains information about the cog and how to use it. I have potential plans in the
future to add a command to the base of the bot will use a `HELP.md` file in the root of the repository to display help
information about a specific cog.
- `requirements.txt` contains the python packages which are required to run the cog.