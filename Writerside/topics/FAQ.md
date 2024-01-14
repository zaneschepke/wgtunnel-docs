# FAQ

This sections details commonly asked questions and the answers to those questions.

### Is %product% supported on AndroidTV?

Yes, the app is generally supported on AndroidTV, however, it was never designed
for AndroidTV. This can result is a somewhat clunky user experience. 

### How do I add a tunnel?

To add a tunnel, you need either a WireGuard server or a VPN Provider that allows you to export
tunnel configs for third party apps. This will be in the form of a `.conf` file or a QR code.

### Does %product% work with Android Auto? 

Yes, %product% works with Android Auto, but this requires some configuration.
You need to disable tunneling for the Android Auto app by leveraging the app's split tunneling feature.
For more information on how to do this, see the [Split Tunneling](Features.md#split) section. This will effectively disable Android Auto app traffic from passing through the tunnel, 
while still tunneling the app traffic for all of your other apps. 


### Why are some feature not available for AndroidTV? {id="tv-features-faq"}

Unfortunately, AndroidTV does not have all the same API and security features as Android mobile. 
For this reason, some features are disabled for AndroidTV.