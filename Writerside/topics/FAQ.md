# FAQ

This section details commonly asked questions and the answers to those questions.

### Is %product% supported on AndroidTV?

Yes, the app is generally supported on AndroidTV, however, it was never designed
for AndroidTV. This can result in a somewhat clunky user experience. 

<warning>
    <p>
        Amazon's FireTV is no longer supported by %product%. See <a href="#firetv-faq">here</a> for details.
    </p>
</warning>

### How do I add a tunnel?

To add a tunnel, you need either a WireGuard server or a VPN Provider that allows you to export
tunnel configs for third party apps.
This will commonly be in the form of a <path>.conf</path> file or a QR code.

### Does %product% work with Android Auto? 

Yes, %product% works with Android Auto, but this requires some configuration.
You need to disable tunneling for the Android Auto app by leveraging the app's split tunneling feature.
For more information on how to do this, see the [Split Tunneling](Features.md#split) section. This will effectively disable Android Auto app traffic from passing through the tunnel, 
while still tunneling the app traffic for all of your other apps. 


### Why are some features not available for AndroidTV? {id="tv-features-faq"}

Unfortunately, AndroidTV does not have all the same API and security features as Android mobile. 
For this reason, some features are disabled for AndroidTV.

### Do %product% support Amazon's FireTV? {id="firetv-faq"}

There is an older version of the app on the Amazon App Store, but it is no longer supported. 
It became clear that supporting the FireTV was going to be impossible for two main reasons:

1. FireTV's broken file selector API. The only way around to this is to reinvent the wheel and build a custom file selector UI from scratch.
2. Poorly implemented developer portal with almost no support, a painful review process, and zero CI for apps.

That being said, the app can still be side-loaded on a FireTV. 
The app will likely work. 
As for broken file selector,
I have heard reports that an app called [Android TV ADB Maus](https://play.google.com/store/apps/details?id=svarzee.android.apps.adb_mouse&amp;hl=en_US&amp;gl=US)
allows for navigation of the file selector screen and import configs.

### Why does %product% require location permissions for auto-tunneling? 

Android has deemed Wi-Fi SSIDs as precise location information. 
In order for %product% to read the SSID from the system, it must have these permissions.

<note>
    <p>
        This permission is only required if you enable <em>Tunnel on untrusted wifi</em> in the auto-tunneling settings.
    </p>
</note>

### How do I exclude my local network from the tunnel so I can access my local services and devices?

There is a handy tool
that exists
for properly generating the allowedIps configuration [here](https://www.procustodibus.com/blog/2021/03/wireguard-allowedips-calculator/). 

Once you add the address block(s) to be ingored by the tunnel, 
generate the allowedIps list and paste the output to the allowIps field on your tunnel config.   

<seealso>
    <category ref="wrs">
        <a href="https://github.com/zaneschepke/wgtunnel">GitHub project</a>
        <a href="https://github.com/zaneschepke/wgtunnel/releases">Changelog</a>
    </category>
</seealso>
