# Getting started

It is important to understand that %product% is a <tooltip term="vpn_client">VPN client</tooltip> application and not a 
<tooltip term="vpn_service">VPN service</tooltip> provider. In short, this means that this application does not provide
a VPN server for users to connect to by default. It is expected that the user either is hosting their own VPN server, or
they are paying a <tooltip term="vpn_service">VPN service</tooltip> provider. 

If you are new to using VPNs and do not yet have a <tooltip term="vpn_service">VPN service</tooltip> provider or VPN server,
one of the easiest ways to get started is with a free <tooltip term="vpn_service">VPN service</tooltip> provider like <a href="https://protonvpn.com/">ProtonVPN</a>.

<warning>
    <p>
        I do not personally use <a href="https://protonvpn.com/">ProtonVPN</a>, nor am I advocating for using their services.
        The reason I am referencing this company in these docs is because they happen to be a well-known VPN provider with a free tier and an
        easy method for exporting <a href="https://www.wireguard.com/">WireGuard</a> configurations.
        It is <format style="bold">highly recommended</format> you do your own research on which VPN provider you want to use as you are trusting them with access to
        to your sensitive internet traffic data. 
    </p>
</warning>

### Steps for getting a WireGuard config: 
- Create a new account on <a href="https://protonvpn.com/">ProtonVPN</a>'s site.
- Follow their <a href="https://protonvpn.com/support/wireguard-configurations/">tutorial</a> on how to export a <a href="https://www.wireguard.com/">WireGuard</a> configuration file.
- On the main screen of %product%, click the floating action button and select "Add from file or zip".
- Navigate to your newly downloaded <a href="https://www.wireguard.com/">WireGuard</a> configuration file and select it.

You are now ready to start using %product% as your Android VPN client.

