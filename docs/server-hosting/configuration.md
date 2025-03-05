# Server Configuration

This guide explains how to configure network settings for your Chivalry 2 Unchained server using Unreal Engine 4's configuration system.

All config files can be found in `%localappdata%/Chivalry 2/Saved_UnchainedServer/Config/WindowsNoEditor/Engine.ini`

!!! Ensure your server has been shut down before making any ini modifications! Failure to do so will cause your changes to be overwritten!

## Engine.ini Settings

### IpNetDriver

```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=60
MaxClientRate=100000
MaxInternetClientRate=100000
InitialConnectTimeout=300.0
ConnectionTimeout=300.0
```

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

!!! Recommended values are still being worked on. Play with them and see what works best for you. Report your results to the community and we will update this doc!

For more UE4 network settings, see the [Unreal Engine Networking Documentation](https://docs.unrealengine.com/4.25/en-US/InteractiveExperiences/Networking/Overview/).

## Game.ini Settings

### Increase Max Player Count

```ini
[/Script/Engine.GameSession]
MaxPlayers=256
```

### Enable Bot Backfill

```ini
[/Script/TBL.TBLGameMode]
BotBackfillEnabled=True
BotBackfillLowPlayers=10
BotBackfillLowBots=12
BotBackfillHighPlayers=30
BotBackfillHighBots=0
```

### Change Server Name

The name displayed in upper left corner when you press Tab ingame

```ini
[/Script/TBL.TBLGameMode]
ServerName=My Local server
```

### Reduce Warmup Time

```ini
[/Script/TBL.TBLGameMode]
MinTimeBeforeStartingMatch=1.000000
```

### Disable/Change AFK Timers

```ini
[/Script/TBL.TBLGameMode]
IdleKickTimerSpectate=0.000000
IdleKickTimerDisconnect=0.000000
```

### Change Map List

Default map list below:

```ini
[/Script/TBL.TBLGameMode]
Maplist=FFA_Wardenglade
Maplist=FFA_TournamentGrounds
Maplist=FFA_Courtyard
Maplist=FFA_Galencourt
MapListIndex=-1
```

### Allow Horses

```ini
[/Script/TBL.TBLGameMode]
bHorseCompatibleServer=true
```
