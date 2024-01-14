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

1. Upload a `.conf` file
2. Upload a zip containing `.conf` files (like an export from %product% or the official app)
3. Scan a QR code <a href="FAQ.md#tv-features-faq"><emphasis>(Mobile only)</emphasis></a>
   - This option will upload the tunnel with a randomly generated name.
4. Create one from scratch

## Auto-tunneling

Coming soon!

## Split tunneling {collapsible="true"} {id="split"}

Split tunneling is a feature that allows a user to route only selected app's traffic through the tunnel.
Currently, this is configured on a per-tunnel basis. 

A common use-case could be
that a user wants apps that only function in another country
to be tunneled to a VPN server in that country while all other apps use the normal network.

## Always-on VPN  {id="always-on-feature"}

<a href="FAQ.md#tv-features-faq"><emphasis>(Mobile only)</emphasis></a>

Coming soon!

## Exporting tunnel configs {id="export-feature"}

<a href="FAQ.md#tv-features-faq"><emphasis>(Mobile only)</emphasis></a>

%product% offers the ability to export all of your tunnel configurations to a zip folder. 

1. Navigate to the <emphasis>Settings</emphasis> screen.
2. Click `Export configs` near the bottom of the screen.
3. Complete the biometrics prompt.
4. All configs are now saved to the <emphasis>Downloads</emphasis> folder on your device in a zip folder called `wg-export_<timestamp>.zip`. 


## Auto restart on boot

Auto start on boot is automatically enabled when a user enables auto-tunneling. 
This feature will automatically restart the auto-tunneling service on boot if the phone has been shutdown or rebooted.

<note>
    <p>
        It can sometimes take up to a few minutes after boot for the service be started by Android.
    </p>
</note>

## Battery saver (beta)

This feature shortens the wakelock timer for %product% to prevent it from draining the battery.

- Timer with battery saver: 10-minutes
- Timber without battery saver: 30-minutes

<seealso>
    <category ref="wrs">
        <a href="https://github.com/zaneschepke/wgtunnel">Github project</a>
        <a href="https://github.com/zaneschepke/wgtunnel/releases">Changelog</a>
    </category>
</seealso>
