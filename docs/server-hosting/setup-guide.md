# Setting up an Unchained Server

!!! warning "Important"
    Excessive modification of ini files or other mods before starting this may cause issues. If you have problems, try completely deleting `%localappdata%/Chivalry 2` and reinstalling Chivalry 2 before doing this tutorial again. Frequently back-up known-good INI configurations as you make changes to avoid having to start over.

## Definitions

| Term | Definition |
|------|------------|
| **Host machine** | The computer hosting the Chivalry 2 server |
| **Host instance** | The instance of Chivalry 2 acting as the "server." A single machine may run Chivalry 2 twice, with one instance running as a client and the other as a server |
| **Client instance** | See above, but it's a client instead |
| **Backend** | An instance of our [C2ServerBrowserBackend](https://github.com/Chiv2-Community/C2ServerBrowserBackend). We run one at `servers.polehammer.net`, so you don't have to. This imitates portions of the PlayFab API to send custom MOTD and server list results to clients that target it |

## Requirements

Before starting, ensure you have:

- A public IP address that you can forward ports to (if you want to host a public server on the internet)
- A bare-metal NIC (Network Interface Card) on the host machine
- Chivalry 2 installed on the host machine

## Initial Setup

1. Install Unchained on the host as you normally would. Make sure Unchained is replacing the normal Chivalry 2 launcher. (You will be prompted to do this on install)
2. Go to the 'Server' tab of the Unchained Launcher and enter your server's name and other configuration

If Chivalry 2 has not run on this machine before, or you deleted `%localappdata%/Chivalry 2/Saved_UnchainedServer`:

1. Click "Launch Headless" in the bottom right
2. Let this run for ~20 seconds to ensure that ini files are generated
3. Close all windows that opened
4. You may be prompted to download several files: Click "Yes"

!!! warning "Important for NFO Hosts"
    If you are using NFO hosting, there is a port conflict with UDP/7777. Change your game port to 7778 in the server tab. No other action is needed. If you do not do this then you will experience extreme gameplay degradation.

## Necessary ini Tweaks

There are two ini settings that must be set in order to successfully host:

1. Navigate to `%localappdata%/Chivalry 2/Saved_UnchainedServer/Config/WindowsNoEditor` in your file browser
2. Open `Game.ini`
3. Add the following lines to the top of the file:

```ini
[/Script/TBL.TBLGameInstance]
FirstLoadCompleted=True

[/Script/TBL.TBLTitleScreen]
bSavedHasAgreedToTOS=True
```

!!! note
    If the TBLGameInstance or TBLTitleScreen sections are already present somewhere in the file, add the lines to those sections instead of making a duplicate.

## Recommended Configuration Settings

While the above settings are the minimum required to get your server running, you'll likely want to customize your server further. Here are some important configuration values to consider:

### Server Identity and Player Limits

In `Game.ini`, under the `[/Script/TBL.TBLGameMode]` section:

??? example "Server Identity Configuration"
    ```ini
    # Server Name (displayed in-game)
    ServerName=My Awesome Server
    ServerIdentifier=MyServer

    # Player Limits
    [/Script/Engine.GameSession]
    MaxPlayers=64
    ```

### Performance and Synchronization

In `GameUserSettings.ini`, under the `[/Script/TBL.TBLGameUserSettings]` section:

??? example "Performance Configuration"
    ```ini
    # FPS settings (important for netcode synchronization)
    MaxFPS=80
    FrameRateLimit=80.000000
    ```

!!! important "FPS Synchronization"
    The FPS setting is critical for proper gameplay. Players should match their FPS to your server's setting to avoid desync issues. Advertise your FPS cap in your server name.

### Bot Backfill

In `Game.ini`, under the `[/Script/TBL.TBLGameMode]` section:

??? example "Bot Configuration"
    ```ini
    # Bot settings
    BotBackfillEnabled=True
    BotBackfillLowPlayers=10
    BotBackfillLowBots=12
    BotBackfillHighPlayers=30
    BotBackfillHighBots=0
    ```

### Team Balance

In `Game.ini`, under the `[/Script/TBL.TBLGameMode]` section:

??? example "Team Balance Configuration"
    ```ini
    # Team balance settings
    TeamBalanceOptions=(MinNumPlayers=0,MaxNumPlayers=32,AllowedNumPlayersDifference=2)
    TeamBalanceOptions=(MinNumPlayers=32,MaxNumPlayers=48,AllowedNumPlayersDifference=3)
    TeamBalanceOptions=(MinNumPlayers=48,MaxNumPlayers=999,AllowedNumPlayersDifference=3)
    AutoBalanceOptions=(MinNumPlayers=0,MaxNumPlayers=24,AllowedNumPlayersDifference=1)
    AutoBalanceOptions=(MinNumPlayers=24,MaxNumPlayers=999,AllowedNumPlayersDifference=2)
    StartOfMatchGracePeriodForAutoBalance=30
    StartOfMatchGracePeriodForTeamSwitching=0
    bUseStrictTeamBalanceEnforcement=False
    ```

For a complete list of configuration options and detailed explanations, see our [Server Configuration Guide](configuration.md).

## Launching

Go back to the server tab in the Unchained Launcher and click "Launch Headless". You may be prompted to download several files: Click "Yes". 

Two windows will open:

1. **The Unchained debug window** - which you will see during normal Unchained launches
2. **Your server's RCON control panel** - which registers your server with the Unchained backend (so that it appears in the Unchained in-game server list) and allows you to execute server commands

These commands are from the same list as the in-game console.

For advanced server configuration options, including network settings, see our [Server Configuration Guide](configuration.md).

For information on how to moderate your server, including kicking and banning players, see our [Server Moderation Guide](moderation.md).

## Port Forwarding

!!! success "NFO Hosts"
    NFO servers have automatic port forwarding—you don't have to do anything here.

Before anyone other than you can join your server, you need to forward your ports (expose them to the open internet).

### Required Ports

| Port | Protocol | Purpose |
|------|----------|---------|
| 7777 | UDP | Game Port (default) |
| 3075 | UDP | Ping Port (default) |

### Additional Ports (Do Not Forward to Internet)

| Port | Protocol | Purpose | Notes |
|------|----------|---------|-------|
| 9001 | TCP | RCON port | **DO NOT expose to internet!** |
| 7071 | UDP | A2S port | Internal use only |

!!! danger "Security Warning"
    ***The RCON port (TCP/9001) should not be exposed to the open internet!*** Doing this would give anyone full freedom to execute admin commands on your server! They (likely) can't hack your machine through this, but they *can* ban people, kick people, and change the map to whatever they want! 
    
    If you want your admins accessing this, use [SSH tunneling](https://www.ssh.com/academy/ssh/tunneling-example) or set up your firewall rules to allow only specific IPs.

The ports you need to forward are visible (and can be changed to whatever you want before launching) in the server tab of the Unchained Launcher. Doing this follows the same procedure as forwarding ports for any other game, and thus will not be described here. Tutorials for port forwarding can be found online.

## Troubleshooting

### A2S Timed Out

On the initial start of your server, these messages are normal. The console attempts to connect to the Chivalry server before it has actually had time to start up and listen. If these messages do not stop appearing after ~30 seconds, then there is something wrong.

#### Troubleshooting Steps:

1. Try sending a console command
   
    **If you get an error in the server console:**
    - This means that the Chivalry process is not listening on RCON
    - This indicates a plugin loading issue
    - Close the server windows and re-start it
    - If the issue persists, contact the Unchained Team for help
   
    **If you see the same console command appear in the debug output window:**
    - This indicates that the plugins are loaded, but the server has not yet loaded into the map to listen on the A2S port
   
    - Check if there is a "Substituted console command" line in the debug output
        - If there is one, contact the Unchained Team—this indicates there is an issue in the Unchained-Mods and map loading machinery
        - If there is no "Substituted console command" line, this suggests an ini misconfiguration
        - Go to the *Necessary ini Tweaks* section and ensure the required ini lines are present
        - If you keep having trouble, contact the Unchained Team

### Severe Network Lag

!!! warning "NFO hosts"
    Make sure your game port is NOT 7777. Change it to 7778.

!!! tip "Other hosts"
    Make sure you don't have any applications using UDP/7777 on your computer.

## Known Issues

1. **Animation Bugs**
   - For the host instance, animations are bugged
   - There is no workaround for this other than launching another instance, joining as a client, and playing on that instead

2. **FPS Sensitivity**
   - Netcode is very sensitive to host and client FPS
   - It is strongly recommended that you cap the fps of the host instance, and advertise that fps in your server description
   - Clients should lock their fps to match
   - If the host is running at, for example, 120fps:
     * Clients running at lower (<120) fps will get delayed hits, swing-throughs, and other netcode issues
     * Clients running at higher (>120) fps will get accelerated/early hits

## Quick Configuration Checklist

Before launching your server, ensure you've configured these essential settings:

### Basic Setup
- [ ] Set `FirstLoadCompleted=True` and `bSavedHasAgreedToTOS=True` in Game.ini
- [ ] Configure your server name and identifier
- [ ] Set appropriate max player count
- [ ] Configure FPS cap (recommended: 60-80)
- [ ] Set up map rotation

### Network & Security
- [ ] Forward required ports (Game Port and Ping Port)
- [ ] Secure RCON port from public access
- [ ] For NFO hosts: Change game port from 7777 to 7778

### Gameplay Settings
- [ ] Configure team balance settings if hosting team-based modes
- [ ] Set up bot backfill if desired
- [ ] Familiarize yourself with [server moderation commands](moderation.md)

### For LTS/Arena Servers
- [ ] Set appropriate round count and time limits
- [ ] Configure team lives if desired
