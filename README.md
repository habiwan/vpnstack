# vpnstack
docker portainer stack for WireGuard VPN + duckDNS + AdGuard Home + Nginx Proxy Manager

What this allows you to do is access your home local LAN securely and for free without any hassle configuring certificates or anything like that...

A few steps and you can then install the WireGuard Client on any of your devices to be like "sitting at home" while away from the house (Yes that includes mobile connections!)
see <a href>https://www.wireguard.com/install/<a> for the client downloads...

Even if you have a Dynamic IP Address thanks to Duckdns free DDNS forwarding system. If you have a static IP address this is still useful as NPM would allow you to expose securely with let's encrypt self signed duckdns certificates any subdomain you want to any internal local IP address and port (TCP only for html)... but this is awesome becasue you do not have to struggle signing certificates, or configuring this via a cumbersome WebUI... NPM is super straight forward and easy!

If you do not need the NPM functionality you can ignore all of it in the config and steps below...

I use this to be able to remote control my MacOS and Linux and Windows devices via RDP, very similar to steam link, high quality and audio!
See <a href>https://rustdesk.com/docs/en/self-host/rustdesk-server-oss/docker/</a> for the local server and <a href>https://github.com/rustdesk/rustdesk/releases/</a> for the clients. It all stays local, no need to create an account with rustdesk or open a port in your router firewall for this... It is as if you're "sitting at home"!!!

1. Go to duckdns.org and create your free DDNS account you cheapskate!
2. Choose a domain, if you can get it it's unique and yours, e.g. EXAMPLE.duckdns.org
3. Copy the token from your duckdns.org account (and the full DDNS domain obviously... like EXAMPLE.duckdns.org)
4. Install docker on your PC or VM (I prefer a Full Ubuntu Desktop 25.10 VM on a Proxmox VE... but hey that's just me...)
5. Install portainer CE (Community Edition) in that VM <a href>https://docs.portainer.io/start/install-ce/server/docker/linux</a>
6. Open portainer, typically <a href>https://YOURUBUNTUVMIPADDR:9443/</a> and create your local admin account
7. Go to your Environment and open "Stacks", create a new stack and name it (e.g. MYVPNSTACKPANTS)
8. Copy + paste the content of the vpnstack.yaml into the editor. (IF using ARM processors like M4 Macs or Raspbeey Pi's change :latest to what works for you)
9. Scroll down a little bit and click on the "Advanced Mode" stack.env editing to add the content of stack.env
    a. Put your duckdns domain and token in there
    b. Put your local Router IP Adress in there (under global DNS)
    c. Put your DDNS.duckdns.org again in the public IP this time!!!
10. Deploy the stack
11. Go to <a href>http://YOURUBUNTUVMIPADDR:10086</a> to create an admin user for WireGuard and enable wg0
12. Go to <a href>http://YOURUBUNTUVMIPADDR:81</a> to create an admin user for NPM and create your different subdomains (e.g. pants.YOURDDNSFROM.duckdns.org)
13. Go to <a href>http://YOURUBUNTUVMIPADDR:82</a> to create an admin user for AdGuard Home
14. In your Router, forward the following ports to your YOURUBUNTUVMIPADDR: (sometimes called port mapping sometimes NAT)
    a. Port 51820 for WireGuard VPN
    b. Port 80 for NPM
    c. Port 443 for NPM(SSL)
15. In your Router, find the DNS config and force DNS1 to be YOURUBUNTUVMIPADDR, DNS2 can be 1.1.1.1 for example...
