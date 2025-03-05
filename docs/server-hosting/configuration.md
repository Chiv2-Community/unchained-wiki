# Server Configuration

This guide explains how to configure network settings for your Chivalry 2 Unchained server using Unreal Engine 4's configuration system.

## Engine.ini Location

```
%localappdata%/Chivalry 2/Saved_UnchainedServer/Config/WindowsNoEditor/Engine.ini
```

## IpNetDriver Settings

Add the following section to your Engine.ini file:

```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=60
MaxClientRate=100000
MaxInternetClientRate=100000
InitialConnectTimeout=300.0
ConnectionTimeout=300.0
```

## Key Network Parameters

| Parameter | Description | Recommended Values |
|-----------|-------------|-------------------|
| NetServerMaxTickRate | Server updates per second | 30 (low), 60 (balanced), 120 (high) |
| MaxClientRate | Max bytes/sec to LAN clients | 50000 (low), 100000 (balanced), 150000 (high) |
| MaxInternetClientRate | Max bytes/sec to internet clients | 50000 (low), 100000 (balanced), 150000 (high) |
| InitialConnectTimeout | Seconds to establish connection | 300.0 |
| ConnectionTimeout | Seconds before disconnect | 300.0 |
| LanServerMaxTickRate | Max tick rate for LAN | Same as NetServerMaxTickRate |
| RelevantTimeout | Actor relevance timeout | 5.0 |
| SpawnPrioritySeconds | Spawn priority window | 1.0 |
| ServerTravelPause | Map change pause | 4.0 |

## Recommended Configurations

### Balanced (60 FPS)
```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=60
MaxClientRate=100000
MaxInternetClientRate=100000
```

### High Performance (120 FPS)
```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=120
MaxClientRate=150000
MaxInternetClientRate=150000
```

### Low Resource (30 FPS)
```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=30
MaxClientRate=50000
MaxInternetClientRate=50000
```

## Important Notes

1. **Advertise your tick rate** in your server description so players can match their FPS
2. **Higher tick rates need more CPU power** - ensure your hardware can handle it
3. **Higher rates need more bandwidth** - check your connection can support MaxInternetClientRate × player count
4. **Restart your server** after changing these settings

For more UE4 network settings, see the [Unreal Engine Networking Documentation](https://docs.unrealengine.com/4.27/en-US/InteractiveExperiences/Networking/Overview/).
