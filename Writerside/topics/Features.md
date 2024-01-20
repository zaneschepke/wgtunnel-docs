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



## Auto-tunneling

Auto-tunneling is the core feature of the application. 
It allows users to automate under which network circumstances a tunnel will activate.

A core concept when using auto-tunneling is setting a <tooltip term="primary_tunnel">primary tunnel</tooltip>.

Setting a primary tunnel can be accomplished by doing a long-press on the desired tunnel config on the main screen
and clicking the <emphasis>star icon</emphasis>.

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

## Auto-tunneling override

Auto-tunnel override is a feature of %product% that allows users to temporarily 
pause (override) [auto-tunneling](#auto-tunneling) to toggle a tunnel.

The status of the override can be viewed on the main screen of the app when [auto-tunneling](#auto-tunneling) is enabled.

<img src="override.png" alt="override" border-effect="line"/>

There are two statuses:
- <control>active</control>: [auto-tunneling](#auto-tunneling) is active and controlling tunnel state
- <control>paused</control>: [auto-tunneling](#auto-tunneling) is paused by the user who can now toggle tunnels freely without fully turning off [auto-tunneling](#auto-tunneling) from the settings screen.

This feature can be activated three different ways:

1. Clicking the <emphasis>pause</emphasis> button from the main screen
2. Toggling a tunnel via [quick tile](#quick-tile-settings)
3. Toggling a tunnel via [shortcut/intent](Integrations.md)

It is common for users to need to manually toggle a tunnel quickly in certain situations when auto-tunneling is active. 
This temporary override was created to meet this need.

## Split tunneling {collapsible="true"} {id="split"}

Split tunneling is a feature that allows a user to route only selected app's traffic through the tunnel.
Currently, this is configured on a per-tunnel basis. 

A common use-case could be
that a user wants apps that only function in another country
to be tunneled to a VPN server in that country while all other apps use the normal network.

## Auto restart on boot

Auto start on boot is automatically enabled when a user enables auto-tunneling.
This feature will automatically restart the auto-tunneling service on boot if the phone has been shutdown or rebooted.

<note>
    <p>
        It can sometimes take up to a few minutes after boot to start the service.
    </p>
</note>

## Battery saver (beta)

This feature shortens the wakelock timer for %product% to prevent it from draining the battery.

- Timer with battery saver: 10-minutes
- Timer without battery saver: 30-minutes


## Tunnel statistics

Clicking on a tunnel while it is running will show per peer tunnel statistics including:
- Rx in MB
- Tx in MB
- Last successful handshake in seconds
- First characters of peer public key

<img src="statistics.png" alt="statistics" border-effect="line"/>

## Quick tile settings

Quick tile settings is a feature of %product% that allows users to quickly control and
see the status of the active tunnel without opening the app. 

<img src="quick-tile.png" alt="quick-tile" border-effect="line"/>

Even if [auto-tunneling](#auto-tunneling) is enabled,
toggling the quick tile will temporarily disable [auto-tunneling](#auto-tunneling) via the
[auto-tunneling override](#auto-tunneling-override) feature to allow users to temporarily turn the tunnel on or off.

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
        <a href="https://github.com/zaneschepke/wgtunnel">Github project</a>
        <a href="https://github.com/zaneschepke/wgtunnel/releases">Changelog</a>
    </category>
</seealso>
