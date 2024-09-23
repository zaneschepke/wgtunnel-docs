# Features

This section details all the app's existing features and behaviors. 

<note>
    <p>
        Some features are only available on mobile and will be marked 
<a href="FAQ.md#tv-features-faq"><emphasis>(Mobile only)</emphasis></a>.
    </p>
</note>

## Adding tunnel configs
There are multiple ways tunnel configs can be added to the app.

After clicking the floating action button on the main screen, the following options are available:

1. Upload a <path>.conf</path> file
2. Upload a zip containing <path>.conf</path> files (like an export from %product% or the official app)
3. Scan a QR code <a href="FAQ.md#tv-features-faq"><emphasis>(Mobile only)</emphasis></a>
   - This option will upload the tunnel with a randomly generated name.
4. Create one from scratch

## AmneziaWG Support

%product% fully supports a fork of WireGuard called [AmneziaWG](https://docs.amnezia.org/documentation/amnezia-wg). [AmneziaWG](https://docs.amnezia.org/documentation/amnezia-wg) is based off of WireGuard,
but adds obfuscation to WireGuard's packet signatures to prevent deep packet inspection (DPI) systems from censoring WireGuard traffic.

One of the key differences (from a user perspective) between WireGuard and Amnezia is Amnezia adds additional properties to the standard WireGuard configuration format. 
Without these properties populated, Amnezia will fall back to using standard WireGuard and the packet signature obfuscation will not be applied. 

> It is important to note that Amnezia only supports userspace mode on Android and not kernel mode.

### How to convert an existing WireGuard config to Amnezia

1. Open the tunnel setting screen by long pressing on a tunnel and clicking the gear icon.
2. Click the edit tunnel floating action button and select the Amnezia option.
3. The shared WireGuard properties will already be populated. Populate the addition empty Amnezia
properties with the follwing data:

Junk packet count: between 3-5 (can be anywhere between 1-128) \
Junk packet minimum size: 40 \
Junk packet maximum size: 70 \
Init packet junk size: 0 \
Response packet junk size: 0 \
Init magic packet header: 1 \
Response packet magic header: 2 \
Underload packet magic header: 3 \
Transport packet magic header: 4

Alternatively, these values can be added to the .conf file before import:
```
[Interface]
Address = ***
PrivateKey = ***
DNS = ***
MTU = ***
Jc = 4
Jmin = 40
Jmax = 70
S1 = 0 
S2 = 0 
H1 = 1 
H2 = 2 
H3 = 3 
H4 = 4 
```

<warning>
    <p>
      For better censorship resistance,
optionally set S1 and S2 between 2 and 10 but this breaks WireGuard server compatibility. 
    </p>
</warning>


When using an Amnezia server, this values will be different and should match the server values.

## Auto-tunneling

Auto-tunneling is the core feature of the application. 
It allows users to automate which tunnel will be active under certain network circumstances.

A core concept when using auto-tunneling is setting a <tooltip term="primary_tunnel">primary tunnel</tooltip>.

Setting a primary tunnel can be accomplished by doing a long-press on the desired tunnel config on the main screen
and clicking the <emphasis>gear icon</emphasis>.

<note>
    <p>
        Setting a <tooltip term="primary_tunnel">primary tunnel</tooltip> is not strictly required
as the app will automatically select a default tunnel if one does not already exist.
Additionally, <a anchor="always-on-feature">Always-On VPN</a> is disabled in this mode to prevent conflicts.
    </p>
</note>

There are three auto-tunneling modes that can be used in combination or individually:

1. <control> Tunnel on mobile data </control>
   - The app detects when the device has switched to using mobile data and turns on the tunnel.
   - <emphasis>Common use case:</emphasis> Connecting to home server whenever leaving the house
2. <control> Tunnel on ethernet </control>.
   - The app detects when a device has switched to an ethernet connection and turns on the tunnel.
   - <emphasis>Common use case:</emphasis> AndroidTV devices (especially portable ones)
3. <control> Tunnel on untrusted wifi </control> <emphasis>(Location required)</emphasis>
   - The app detects when the device has connected to a new Wi-Fi network. 
   If the network name (SSID) is not in the list of trusted network names, start the tunnel.
   - <emphasis>Common use case:</emphasis> Disable the tunnel on my home (trusted) network, 
   but enable it when I connect to any public Wi-Fi network.

### Wildcard Wi-Fi name support

Trusted Wi-Fi names and tunnel specific Wi-Fi name now support wildcards.

Allowed wildcards:
- Use \* to allow any number of characters after or before a given string segment. <emphasis>Example:</emphasis> "Guest*" will match all Wi-Fi names that start with Guest".
- Use ? to allow a single wildcard character. <emphasis>Example:</emphasis> "Guest?" will match any Wi-Fi with the name "Guest" and one additional wildcard character.
- Use ! to mark Wi-Fi name to be excluded. <emphasis>Example:</emphasis> A common use case for this flag would be to use it in combination with a "*" (all Wi-Fi names) "!Guest". This would trust all Wi-Fi names and exclude "Guest" from this trusted list. 


### Auto-tunneling to a specific tunnel by wifi name and/or mobile data

A common scenario is when a user wants to use a specific tunnel config when they are connected to certain networks.

> For example,
a user might want to connect to their home VPN server when they are away from home
and then want to connect to their VPN provider's server while at home.

%product% now allows users to configure each tunnel to be used on specific Wi-Fi networks and/or mobile data.
Tunnels configured with these settings will be prioritized over the primary tunnel if the app detects a match.

To configure:
- Long press on the tunnel config you would like to configure from the main screen
- Click the gear icon
- Add a Wi-Fi name where you would like to prioritize using this tunnel or turn on mobile data if this is your mobile data specific tunnel.

%product% auto-tunneling will now prioritize using this specific tunnel if it detects a matching network scenario. 


### Auto-tunneling pausing

Auto-tunnel pause is a feature of %product% that allows users to temporarily 
pause [auto-tunneling](#auto-tunneling).

This feature may be useful
when a user wants
to quickly make a change to a tunnel or quickly disable [auto-tunneling](#auto-tunneling) without completely shutting it down. 

The status of the pause can be viewed on the main screen of the app when [auto-tunneling](#auto-tunneling) is enabled.

<img src="override.png" alt="pause" border-effect="line"/>

There are two statuses:
- <control>active</control>: [auto-tunneling](#auto-tunneling) is active and controlling tunnel state
- <control>paused</control>: [auto-tunneling](#auto-tunneling) is paused by the user who can now toggle tunnels freely without fully turning off [auto-tunneling](#auto-tunneling) from the settings screen.

This feature can be activated two different ways:

1. Clicking the <emphasis>pause</emphasis> button from the main screen
2. Toggling the auto tunnel [quick tile](#quick-tile-settings)

It is common for users to need to manually toggle a tunnel quickly in certain situations when auto-tunneling is active. 
This temporary override was created to meet this need.

## Split tunneling {collapsible="true"} {id="split"}

Split tunneling is a feature that allows a user to route only selected app's traffic through the tunnel.
Currently, this is configured on a per-tunnel basis. 

A common use-case could be
that a user wants apps that only function in another country
to be tunneled to a VPN server in that country while all other apps use the normal network.

To configure split tunneling: 

1. Long press on a tunnel config to show options
2. Press the gear icon to navigate to the tunnel setting screen
3. Press the pencil floating action button to edit the tunnel config values
4. At the bottom of the Interface section is a <emphasis>Tunneling apps</emphasis> to open the tunneling apps selection dialog.
5. Select which apps to either include or exclude from the tunnel
6. Click <emphasis>Done</emphasis>
7. Click the floating action button to save

## Auto restart on boot

> Auto tunneling will always be restarted automatically on reboot regardless of whether this feature is enabled.

When enabled, auto start on boot will automatically start a tunnel on reboot
in the following order of priority:

1. The last tunnel that was active
2. The primary tunnel
3. The first tunnel in the list of tunnels

<note>
    <p>
        It can sometimes take up to a few minutes after boot to start the tunnel and/or service.
    </p>
</note>

## Auto restart on app update

This feature will automatically restore your running tunnel and/or auto tunnel service after an app update has completed.

## Pre/Post Up/Down Script Support

> This works for all backend modes, but requires a rooted device.

%product% now supports *PreUp, PostUp, PreDown, PostDown* scripts. 

These can be configured as properties in a tunnel <path>.conf</path> file and imported into the app.

For more details and example use cases for these scripts, see the [unofficial docs](https://github.com/pirate/wireguard-docs?tab=readme-ov-file#preup).

## Restart on ping fail (beta)

This feature attempts to restart the tunnel if it is failing to ping your server. 
This feature is still in beta and will likely change in the future.

- Pings vpn server address on an interval: 1-minute(s)
- Cooldown after a failed ping/restart is triggered: 60-minute(s)

## Enable app lock

This feature allows the user to set an app-specific pin when launching WG Tunnel. 

The primary use case for this feature is 
to serve as a parental control mechanism to prevent phone users from being able to disable auto-tunneling.

To config:
- Navigate to app settings
- Toggle "Enable app lock"
- Set your pin

<warning>
    <p>
        Do not forget your pin as there is not a reset feature in the app. 
If you forget your pin, you will have to uninstall and reinstall the app.
    </p>
</warning>

## Tunnel statistics

Clicking on a tunnel while it is running will show per peer tunnel statistics including:
- Rx in MB
- Tx in MB
- Last successful handshake in seconds
- First characters of peer public key

<img src="statistics.png" alt="statistics" border-effect="line"/>

## Quick tile settings

Quick tile settings is a feature of %product% that allows users to quickly control and
see the status of the active tunnel or auto tunneling without opening the app. 

<img src="quick-tile.png" alt="quick-tile" border-effect="line"/>

There are two tiles available. One is for toggling the currently active and/or primary tunnel. 
The other tile is for toggling the state of auto-tunneling from pause/resume.

## Always-on VPN  {id="always-on-feature"}

Turning on the Always-On VPN setting [(mobile only)](FAQ.md#tv-features-faq) in %product% allows the Android OS
to control your <tooltip term="primary_tunnel">primary tunnel</tooltip>
(or an app selected tunnel if no primary is set) through the Android OS Always-On VPN feature.

Android will attempt to keep the tunnel always connected.

<note>
    <p>
        Auto-tunneling is disabled in this mode as it would conflict with the Always-On VPN functionality.
    </p>
</note>

An added benefit to Always-On VPN is the ability to use the <emphasis>Block connections without VPN</emphasis> native Android feature for added security,
but this will prevent split tunneling from working properly.


## Exporting tunnel configs {id="export-feature"}

%product% offers the ability to export all of your tunnel configurations to a zip folder [(mobile only)](FAQ.md#tv-features-faq). 

1. Navigate to the <emphasis>Settings</emphasis> screen.
2. Click `Export configs` near the bottom of the screen.
3. Complete the biometrics prompt.
4. All configs are now saved to the <emphasis>Downloads</emphasis> folder on your device in a zip folder called `wg-export_<timestamp>.zip`.

## Kernel Module Support

If you are on a rooted device, %product% also supports the use of WireGuard's native kernel implementation on Android [(mobile only)](FAQ.md#tv-features-faq). 
This has some performance benefits, but it has been known to be less reliable than the userspace implementation.

<seealso>
    <category ref="wrs">
        <a href="https://github.com/zaneschepke/wgtunnel">GitHub project</a>
        <a href="https://github.com/zaneschepke/wgtunnel/releases">Changelog</a>
    </category>
</seealso>
