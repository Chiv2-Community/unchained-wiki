# Server Configuration

This guide explains how to configure advanced settings for your Chivalry 2 Unchained server. Since Chivalry 2 is built on Unreal Engine 4, many standard UE4 networking configurations apply.

## Network Configuration

UE4 games use the `Engine.ini` file for network configuration. For Chivalry 2 Unchained servers, this file is located at:
```
%localappdata%/Chivalry 2/Saved_UnchainedServer/Config/WindowsNoEditor/Engine.ini
```

### IpNetDriver Settings

The `[/Script/OnlineSubsystemUtils.IpNetDriver]` section in Engine.ini controls how the server handles network traffic. Here are the key settings you can adjust:

#### Basic Settings

```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=60
```

- **NetServerMaxTickRate**: Controls how many times per second the server updates its state (ticks). Higher values provide smoother gameplay but require more CPU and bandwidth. Common values:
  - 30: Minimum recommended for gameplay
  - 60: Good balance between performance and smoothness
  - 120: Excellent responsiveness but higher resource usage

#### Advanced Network Settings

```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=60
MaxClientRate=100000
MaxInternetClientRate=100000
InitialConnectTimeout=300.0
ConnectionTimeout=300.0
```

- **MaxClientRate**: Maximum bytes per second the server will send to clients on a LAN
- **MaxInternetClientRate**: Maximum bytes per second the server will send to clients over the internet
- **InitialConnectTimeout**: How long (in seconds) to wait for a connection to be established
- **ConnectionTimeout**: How long (in seconds) before considering a client disconnected

#### Packet Loss and Latency Handling

```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=60
MaxClientRate=100000
MaxInternetClientRate=100000
InitialConnectTimeout=300.0
ConnectionTimeout=300.0
RelevantTimeout=5.0
SpawnPrioritySeconds=1.0
ServerTravelPause=4.0
```

- **RelevantTimeout**: How long an actor is relevant after becoming irrelevant
- **SpawnPrioritySeconds**: Time window for prioritizing spawning actors
- **ServerTravelPause**: Pause when server travels to new map

#### Lag Compensation

```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=60
MaxClientRate=100000
MaxInternetClientRate=100000
LanServerMaxTickRate=120
```

- **LanServerMaxTickRate**: Maximum tick rate for LAN servers

## Recommended Configurations

### Balanced Configuration (60 FPS)

```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=60
MaxClientRate=100000
MaxInternetClientRate=100000
InitialConnectTimeout=300.0
ConnectionTimeout=300.0
```

### High Performance Configuration (120 FPS)

```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=120
MaxClientRate=150000
MaxInternetClientRate=150000
InitialConnectTimeout=300.0
ConnectionTimeout=300.0
LanServerMaxTickRate=120
```

### Low Resource Usage Configuration (30 FPS)

```ini
[/Script/OnlineSubsystemUtils.IpNetDriver]
NetServerMaxTickRate=30
MaxClientRate=50000
MaxInternetClientRate=50000
InitialConnectTimeout=300.0
ConnectionTimeout=300.0
```

## Important Notes

1. **Advertise Your Settings**: Always mention your server's tick rate in your server description so players can match their client FPS for optimal experience.

2. **CPU Requirements**: Higher tick rates require more CPU power. Make sure your server hardware can handle your chosen settings.

3. **Bandwidth Requirements**: Higher MaxClientRate values require more bandwidth. Ensure your internet connection can support the total bandwidth needed (MaxInternetClientRate × maximum number of players).

4. **Testing**: After changing these settings, thoroughly test your server with a few players before making it public.

## Applying Changes

After modifying your Engine.ini file, you'll need to restart your server for the changes to take effect. No other steps are required.
