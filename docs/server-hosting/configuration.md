# Server Configuration

This guide explains how to configure network settings for your Chivalry 2 Unchained server using Unreal Engine 4's configuration system.

!!! warning "Important"
    Ensure your server has been shut down before making any ini modifications! Failure to do so will cause your changes to be overwritten!

## Configuration File Locations

- Engine.ini: `%localappdata%/Chivalry 2/Saved_UnchainedServer/Config/WindowsNoEditor/Engine.ini`
- Game.ini: `%localappdata%/Chivalry 2/Saved_UnchainedServer/Config/WindowsNoEditor/Game.ini`

## Engine.ini Settings

### `[/Script/OnlineSubsystemUtils.IpNetDriver]`

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

??? example "Example Configuration"
    ```ini
    [/Script/OnlineSubsystemUtils.IpNetDriver]
    NetServerMaxTickRate=60
    MaxClientRate=100000
    MaxInternetClientRate=100000
    InitialConnectTimeout=300.0
    ConnectionTimeout=300.0
    ```

!!! info "Note"
    Recommended values are still being worked on. Play with them and see what works best for you. Report your results to the community and we will update this doc!

For more UE4 network settings, see the [Unreal Engine Networking Documentation](https://docs.unrealengine.com/4.25/en-US/InteractiveExperiences/Networking/Overview/).

## Game.ini Settings

### `[/Script/Engine.GameSession]` Section

| Parameter | Description | Example Value |
|-----------|-------------|---------------|
| MaxPlayers | Maximum number of players allowed on the server | 256 |

??? example "Example Configuration"
    ```ini
    [/Script/Engine.GameSession]
    MaxPlayers=256
    ```

### `[/Script/TBL.TBLGameMode]` Section

#### TBLGameMode Parameters

| Parameter | Description | Example Value |
|-----------|-------------|---------------|
| ServerName | The name displayed in the upper left corner when pressing Tab in-game | MyLocalServer |
| ServerIdentifier | The server identifier displayed in the upper left corner when pressing Tab in-game | id |
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
| TeamBalanceOptions | Team balance settings for player count ranges (MinNumPlayers, MaxNumPlayers, AllowedNumPlayersDifference) | (MinNumPlayers=0,MaxNumPlayers=32,AllowedNumPlayersDifference=2) |
| AutoBalanceOptions | Auto-balance settings for player count ranges (MinNumPlayers, MaxNumPlayers, AllowedNumPlayersDifference) | (MinNumPlayers=0,MaxNumPlayers=24,AllowedNumPlayersDifference=1) |
| StartOfMatchGracePeriodForAutoBalance | Grace period in seconds before auto-balance begins at match start | 30 |
| StartOfMatchGracePeriodForTeamSwitching | Grace period in seconds for team switching at match start | 0 |
| bUseStrictTeamBalanceEnforcement | Enables or disables strict team balance enforcement | False |

??? example "Example Configuration"
    ```ini
    [/Script/TBL.TBLGameMode]
    # Server Name
    ServerName=Example
    ServerIdentifier=id

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
    # LTS Maps
    Maplist=LTS_Falmire
    Maplist=LTS_Courtyard
    Maplist=LTS_Galencourt
    Maplist=LTS_TournamentGrounds
    Maplist=LTS_Wardenglade
    MapListIndex=1

    # Horse Settings
    bHorseCompatibleServer=true

    # Team Balance Settings
    TeamBalanceOptions=(MinNumPlayers=0,MaxNumPlayers=32,AllowedNumPlayersDifference=2)
    TeamBalanceOptions=(MinNumPlayers=32,MaxNumPlayers=48,AllowedNumPlayersDifference=3)
    TeamBalanceOptions=(MinNumPlayers=48,MaxNumPlayers=999,AllowedNumPlayersDifference=3)
    AutoBalanceOptions=(MinNumPlayers=0,MaxNumPlayers=24,AllowedNumPlayersDifference=1)
    AutoBalanceOptions=(MinNumPlayers=24,MaxNumPlayers=999,AllowedNumPlayersDifference=2)
    StartOfMatchGracePeriodForAutoBalance=30
    StartOfMatchGracePeriodForTeamSwitching=0
    bUseStrictTeamBalanceEnforcement=False
    ```

### `[/Script/TBL.TBLTitleScreen]` Section

| Parameter | Description | Example Value |
|-----------|-------------|---------------|
| bSavedHasAgreedToTOS | Bypasses the Terms of Service agreement prompt | True |

??? example "Example Configuration"
    ```ini
    [/Script/TBL.TBLTitleScreen]
    bSavedHasAgreedToTOS=True
    ```

!!! note "Important"
    This setting is necessary for initial setup of headless servers to bypass the Terms of Service prompt. If your server isn't starting, this is likely the cause.

### `[/Script/TBL.LTSGameMode]` Section

| Parameter | Description | Example Value |
|-----------|-------------|---------------|
| PreCountdownDelay | Time in seconds before the match countdown begins | 5 |
| Rounds | Total number of rounds to play (should be N*2-1 where N is the number of rounds to win) | 39 |

??? example "Example Configuration"
    ```ini
    [/Script/TBL.LTSGameMode]
    PreCountdownDelay=5
    Rounds=39
    ```

!!! tip "Rounds Calculation"
    Set Rounds to N*2-1 where N is the number of rounds you want the game to go to. For example, if you want first to 20, use N=20 for Rounds=39.

### `[/Script/TBL.ArenaGameMode]` Section

| Parameter | Description | Example Value |
|-----------|-------------|---------------|
| Rounds | Total number of rounds to play (should be N*2-1 where N is the number of rounds to win) | 39 |
| RoundTimeLimit | Time limit in seconds for each round | 300 |
| bClearWeaponsPostRound | Whether to clear weapons after each round | True |
| bClearHorsesPostRound | Whether to clear horses after each round | True |
| bResetTaggedActorsPostRound | Whether to reset tagged actors after each round | True |
| bUsePreCountdownForCustomizationLoading | Whether to use pre-countdown for customization loading | True |
| MinTimeBeforeStartingMatch | Minimum time in seconds before starting the match | 5 |
| MaxTimeBeforeStartingMatch | Maximum time in seconds before starting the match | 10 |
| TeamLives | Extra lives given to a team (per player) | 0 |

??? example "Example Configuration"
    ```ini
    [/Script/TBL.ArenaGameMode]
    Rounds=39
    RoundTimeLimit=300
    bClearWeaponsPostRound=True
    bClearHorsesPostRound=True
    bResetTaggedActorsPostRound=True
    bUsePreCountdownForCustomizationLoading=True
    MinTimeBeforeStartingMatch=5
    MaxTimeBeforeStartingMatch=10
    TeamLives=0
    ```

!!! info "TeamLives Explanation"
    TeamLives represents extra lives a team gets. For example, in a 6v6 match with TeamLives=1, the first player who dies on each team gets an extra life. With TeamLives=2, the first two players who die get an extra life, and so on.

## GameUserSettings.ini Settings

### `[/Script/TBL.TBLGameUserSettings]` Section

| Parameter | Description | Example Value |
|-----------|-------------|---------------|
| MaxFPS | Maximum frames per second for the server | 80 |
| FrameRateLimit | Frame rate limit in floating point format | 80.000000 |

??? example "Example Configuration"
    ```ini
    [/Script/TBL.TBLGameUserSettings]
    MaxFPS=80
    FrameRateLimit=80.000000
    ```

!!! important "FPS Synchronization"
    MaxFPS is important and should be advertised in your server name. Players will need to match this FPS to avoid desync issues.
