# Server Moderation

This guide explains how to moderate your Chivalry 2 Unchained server by managing players through the RCON console.

## Kicking and Banning Players

To kick or ban a player from your server, follow these steps:

1. In the server's RCON console, run the `listplayers` command
    - This copies all player information to your clipboard

2. Open a text editor (like Notepad), right-click, and select "Paste"
    - This will show a list of all players with their IDs

3. Find the ID of the player you want to moderate
    - The ID appears to the right of their username in ALL CAPS

4. In the RCON console, use one of these commands:
    - To kick: `KickById PLAYER_ID`
    - To ban: `BanById PLAYER_ID`

5. Press Enter to execute the command

## Example

If you see a player named "ToxicPlayer" causing problems:

1. Run `listplayers` in RCON
2. Paste the results in Notepad
3. Find a line like: `ToxicPlayer (ABCD1234)`
4. To kick them, type in RCON: `KickById ABCD1234`
5. To ban them, type in RCON: `BanById ABCD1234`

## Additional Commands

- `UnbanById PLAYER_ID` - Removes a player from the ban list
- `listbans` - Shows all currently banned players

!!! note
    Bans are stored locally on your server. If you reset your server configuration, you may lose your ban list.
