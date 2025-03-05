# Server Configuration

This guide explains how to configure network settings for your Chivalry 2 Unchained server using Unreal Engine 4's configuration system.

!!! Ensure your server has been shut down before making any ini modifications! Failure to do so will cause your changes to be overwritten!

## Configuration File Locations

- Engine.ini: `%localappdata%/Chivalry 2/Saved_UnchainedServer/Config/WindowsNoEditor/Engine.ini`
- Game.ini: `%localappdata%/Chivalry 2/Saved_UnchainedServer/Config/WindowsNoEditor/Game.ini`

## Engine.ini Settings

### IpNetDriver

#### Key Network Parameters

| Parameter | Description | Recommended Values |
|-----------|-------------|-------------------|
| NetServerMaxTickRate | Server updates per second | 30 (low), 60 (balanced), 120 (high) |
| MaxClientRate | Max bytes/sec to LAN clients | 50000 (low), 100000 (balanced), 150000 (high) |
| MaxInternetClientRate | Max bytes/sec to internet clients | 50000 (low), 100000 (balanced), 150000 (high) |
| InitialConnectTimeout | Seconds to establish connection | 60.0 |
| ConnectionTimeout | Seconds before disconnect | 60.0 |
| LanServerMaxTickRate | Max tick rate for LAN | Same as NetServerMaxTickRate |
| RelevantTimeout | Actor relevance timeout | 5.0 |
| SpawnPrioritySeconds | Spawn priority window | 1.0 |
| ServerTravelPause | Map change pause | 4.0 |

```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=60
MaxClientRate=100000
MaxInternetClientRate=100000
InitialConnectTimeout=300.0
ConnectionTimeout=300.0
```

!!! Recommended values are still being worked on. Play with them and see what works best for you. Report your results to the community and we will update this doc!

For more UE4 network settings, see the [Unreal Engine Networking Documentation](https://docs.unrealengine.com/4.25/en-US/InteractiveExperiences/Networking/Overview/).

## Game.ini Settings

### [/Script/Engine.GameSession] Section

| Parameter | Description | Example Value |
|-----------|-------------|---------------|
| MaxPlayers | Maximum number of players allowed on the server | 256 |

```ini
[/Script/Engine.GameSession]
MaxPlayers=256
```

### [/Script/TBL.TBLGameMode] Section

#### TBLGameMode Parameters

| Parameter | Description | Example Value |
|-----------|-------------|---------------|
| ServerName | The name displayed in the upper left corner when pressing Tab in-game | My Local server |
| BotBackfillEnabled | Enables or disables bot backfill feature | True |
| BotBackfillLowPlayers | Player count threshold for maximum bot spawning | 10 |
| BotBackfillLowBots | Number of bots to spawn when player count is at or below the low threshold | 12 |
| BotBackfillHighPlayers | Player count threshold for minimum bot spawning | 30 |
| BotBackfillHighBots | Number of bots to spawn when player count is at or above the high threshold | 0 |
| MinTimeBeforeStartingMatch | Minimum warmup time in seconds before a match starts | 1.000000 |
| IdleKickTimerSpectate | Time in seconds before an idle player is moved to spectator (0 to disable) | 0.000000 |
| IdleKickTimerDisconnect | Time in seconds before an idle player is disconnected (0 to disable) | 0.000000 |
| Maplist | A map to include in the rotation (add multiple lines for multiple maps) | FFA_Wardenglade |
| MapListIndex | Index of the current map in rotation (-1 for random start) | -1 |
| bHorseCompatibleServer | Enables or disables horses on the server | true |

```ini
[/Script/TBL.TBLGameMode]
# Server Name
ServerName=My Local server

# Bot Backfill Settings
BotBackfillEnabled=True
BotBackfillLowPlayers=10
BotBackfillLowBots=12
BotBackfillHighPlayers=30
BotBackfillHighBots=0

# Match Timing
MinTimeBeforeStartingMatch=1.000000

# AFK Timers
IdleKickTimerSpectate=0.000000
IdleKickTimerDisconnect=0.000000

# Map List
Maplist=FFA_Wardenglade
Maplist=FFA_TournamentGrounds
Maplist=FFA_Courtyard
Maplist=FFA_Galencourt
MapListIndex=-1

# Horse Settings
bHorseCompatibleServer=true
```

### [/Script/TBL.TBLTitleScreen] Section

| Parameter | Description | Example Value |
|-----------|-------------|---------------|
| bSavedHasAgreedToTOS | Bypasses the Terms of Service agreement prompt | True |

```ini
[/Script/TBL.TBLTitleScreen]
bSavedHasAgreedToTOS=True
```

!!! note "Important"
    This setting is necessary for initial setup of headless servers to bypass the Terms of Service prompt.
