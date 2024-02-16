---
layout: page
title: PFSENSE WIREGUARD USING NORDLYNX GUIDE 
subtitle: Created by Brian Robert Nokes 2023
---
<h1 style="text-align: center;">SETTING UP PFSENSE WIREGUARD WITH NORDVPN USING NORDLYNX STEP-BY-STEP GUIDE</h1><span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h4 style="text-align: left;">Thank you for taking the time to explore this comprehensive guide. I've invested significant effort into its creation, aiming to provide you with detailed and valuable insights. I trust that you will find it helpful and worthy of sharing with others.</h4>


<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 1</h1>
<h5 style="text-align: left;">VPN/WireGuard/Tunnels</h5>
<h2 style="text-align: left;">The first thing In pfSense, is to navigate to the VPN then WireGuard. Then create a Tunnel.</h2>
<h3 style="text-align: left;">Tunnel Configuration - tun_wg0</h3>
<span style="text-align: left;">Enable Tunnel - check mark on</span>
<br><br>
<span style="text-align: left;">Description</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">WireGuard-Nordvpn</span>
<br><br>
<span style="text-align: left;">Listen Port</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">51820</span>
<br><br>
<span style="text-align: left;">Interface Keys</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">Private key from NordVPN content which goes into Private key for this tunnel. (Required)</span>
<br>
<span style="display: inline-block; margin: 0 50px 0 50px">PrivateKey -<span style="display: inline-block; margin: 0 50px 0 50px">Your Private Key info here</span>
<br><br>
<h2 style="text-align: left;">Save</h2>

<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 2</h1>
<h5 style="text-align: left;">Interfaces/Interface Assignments</h5><br>
<span style="text-align: left;">Interfaces</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">create WG_NordVPN_nordlynx (tun_wg0)</span>
<br><br>
<h3 style="text-align: left;">General Configuration</h3>

<span style="text-align: left;">Enable - Check mark on</span>
<br><br>
<span style="text-align: left;">Description</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NordVPN_nordlynx</span>
<br><br>
<span style="text-align: left;">IPv4</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">Static IPv4</span>
<br><br>
<span style="text-align: left;">IPv4 Address</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">10.5.0.2 /32 - pick anything that you don't have or someone else may not or just keep what NordVPN uses IPv4 Upstream gateway Selecting an upstream gateway causes the firewall to treat this interface as a WAN-type interface. This is a WAN-type interface NordVPN WG_NordVPN_nordlynxGW - 10.5.0.2</span>
<br><br>
<h2 style="text-align: left;">Save</h2>

<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 3</h1>
<h5 style="text-align: left;">VPN/WireGuard/Peers</h5>
<h3 style="text-align: left;">Peers Configuration</h3>
<span style="text-align: left;">Enable Peer - check mark on</span>
<br><br>
<span style="text-align: left;">Tunnel</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">tun_wg0</span>
<br><br>
<span style="text-align: left;">Description</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">WireGuard-Nordvpn</span>
<br><br>
<span style="text-align: left;">Dynamic Endpoint</span>
<span style="display: inline-block; margin: 0 50px 0 50px">Uncheck this option - to assign NordVPN endpoint address and port for this peer, this needs to be off - no check mark</span>
<br><br>
<span style="text-align: left;">Endpoint</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">The Hostname will change when you need a new server</span>
<br><br>
<span style="text-align: left;">Hostname</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">usXXXX.nordvpn.com</span>
<br><br>
<span style="display: inline-block; margin: 0 50px 0 50px">When you see XXXX you need these numbers from nordvpn website server and find what is best but for now, if you want you can use this one for " us8258.nordvpn.com ', and you can use this one for " uk1818.nordvpn.com " "usXXXX.nordvpn.com" - change the XXXX to any number that NordVPN has that you get when you log in from Windows or Linux you should see these numbers and then you can just change the number part if you are using us = USA or here is a sample UK one - uk1818.nordvpn.com</span>
<br><br>
<span style="text-align: left;">Port</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">51820</span>
<br><br>
<span style="text-align: left;">Public Key - From nordvpn peer content</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">Public Key</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">Public Key from NordVPN peer content here</span>
<br><br>
<span style="text-align: left;">Pre-shared Key - Leave blank - optional</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">NA - no Generate</span>
<br><br>
<h3 style="text-align: left;">Address Configuration</h3><br>
<span style="text-align: left;">Allowed IPs</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">0.0.0.0 / 0</span>
<br><br>
<span style="text-align: left;">Description</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">us8258.nordvpn.com:51820</span>
<br><br>
<span style="display: inline-block; margin: 0 50px 0 50px">When you see XXXX you need these numbers from nordvpn website server and find what is best but for now, if you want you can use this one for " us8258.nordvpn.com ', and you can use this one for " uk1818.nordvpn.com " usXXXX.nordvpn.com:51820 - change the XXXX to any number that NordVPN has that you get when you log in from Windows or Linux you should see these numbers and then you can just change the number part if you are using us = USA or here is a sample UK one - uk1818.nordvpn.com</span>
<br><br>
<h2 style="text-align: left;">Save</h2>

<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 4</h1>
<h3 style="text-align: left;">System/Routing/Gateways</h3>
<span style="text-align: left;">now create your Gateway for nordvpn</span><br>
<span style="text-align: left;">Interface</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NORDVPN_NORDLYNX</span>
<br><br>
<span style="text-align: left;">Name</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NordVPN_nordlynxGW</span>
<br><br>
<span style="text-align: left;">Gateway</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">10.5.0.2</span>
<br><br>
<span style="text-align: left;">Description</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">WireGuard-Nordvpn lynx</span>
<br><br>
<span style="text-align: left;">Monitor IP</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">8.8.8.8 or any other IP to see connection in Status / Dashboard widgets name Gateways us this to see Status Online or when its off or not working</span>
<br><br>
<span style="text-align: left;">Description</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">WireGuard-Nordvpn lynx</span>
<br><br>
<h2 style="text-align: left;">Save</h2>

<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 5</h1>
<span style="text-align: left;">When putting it on a VLAN or network</span><br>
<h5 style="text-align: left;">Firewall/NAT/Outbound</h5>
<span style="display: inline-block; margin: 0 50px 0 50px">Mappings</span>
<br><br>
<span style="display: inline-block; margin: 0 50px 0 50px">Create / Add a new one</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">Edit Advanced Outbound NAT Entry</span>
<br><br>
<span style="display: inline-block; margin: 0 50px 0 50px">Interface</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NORDVPN_NORDLYNX</span>
<br><br>
<span style="text-align: left;">Protocol</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">Any</span>
<br><br>
<span style="text-align: left;">Source</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">Type</span><br>
<span style="display: inline-block; margin: 0 50px 0 70px">Network or Alias</span><br>
<span style="display: inline-block; margin: 0 50px 0 90px">176.176.176.0/29</span>
<br><br>
<span style="text-align: left;">Destination</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">Type</span><br>
<span style="display: inline-block; margin: 0 50px 0 70px">Any</span><br>
<h2 style="text-align: left;">Translation</h2><br>
<span style="text-align: left;">Address</span><br>
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NORDVPN_NORDLYNX address

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;"></h1> Step 6
<h5 style="text-align: left;"></h5>Firewall/Rules
<span style="display: inline-block; margin: 0 50px 0 50px">WAN

Action
<span style="display: inline-block; margin: 0 50px 0 50px">Pass

Interface
<span style="display: inline-block; margin: 0 50px 0 50px">WAN

Protocol
<span style="display: inline-block; margin: 0 50px 0 50px">UDP

<h3 style="text-align: left;"></h3>  Source
Source
<span style="display: inline-block; margin: 0 50px 0 50px">Any

<h3 style="text-align: left;"></h3>  Destination
Destination
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NORDVPN_NORDLYNX address
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">This is your interface that you created for the NordVPN WireGuard

Destination Port Range
<span style="display: inline-block; margin: 0 50px 0 50px"> From
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px"> Other
<span style="display: inline-block; margin: 0 50px 0 50px">Custom
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">51820
<span style="display: inline-block; margin: 0 50px 0 50px">To
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">Other
<span style="display: inline-block; margin: 0 50px 0 50px">Custom
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">51820

Description
<span style="display: inline-block; margin: 0 50px 0 50px">Allow WireGuard - 51820

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 7</h1>

<h5 style="text-align: left;"></h5>Firewall/Rules
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NORDVPN_NORDLYNX
Create / Add new Rule

<h3 style="text-align: left;"></h3>  Edit Firewall Rule

Action
<span style="display: inline-block; margin: 0 50px 0 50px">Pass

Interface
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NORDVPN_NORDLYNX

Protocol
<span style="display: inline-block; margin: 0 50px 0 50px">Any
<h3 style="text-align: left;"></h3>  Source
Source
<span style="display: inline-block; margin: 0 50px 0 50px">Any
<h3 style="text-align: left;"></h3>  Destination
Destination
<span style="display: inline-block; margin: 0 50px 0 50px">Any

Description
<span style="display: inline-block; margin: 0 50px 0 50px">Allow All Traffic for WG VPN

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 8</h1>
<h5 style="text-align: left;">Firewall/Rules</h5>
<span style="display: inline-block; margin: 0 50px 0 50px">WireGuard

Action
<span style="display: inline-block; margin: 0 50px 0 50px">Pass

Interface
<span style="display: inline-block; margin: 0 50px 0 50px">WireGuard

Address Family
<span style="display: inline-block; margin: 0 50px 0 50px">IPv4

Protocol
<span style="display: inline-block; margin: 0 50px 0 50px">Any
<h3 style="text-align: left;"></h3>  Source
Source
<span style="display: inline-block; margin: 0 50px 0 50px">Any
<h3 style="text-align: left;"></h3>  Destination
Destination
<span style="display: inline-block; margin: 0 50px 0 50px">Any

Description
<span style="display: inline-block; margin: 0 50px 0 50px">Pass VPN traffic from WireGuard peers

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 9</h1>
<h5 style="text-align: left;">Firewall/Aliases</h5>

Create / Add new Aliases

Name
<span style="display: inline-block; margin: 0 50px 0 50px">Route_Out_Over_NordVPN_lynx

Description
<span style="display: inline-block; margin: 0 50px 0 50px">Route_Out_Over_NordVPN_lynx

Type
<span style="display: inline-block; margin: 0 50px 0 50px">Network(s)
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">Network or FQDN - You can add this to however many networks you need to add this VPN to. I am just using this one VLAN network I created in this example.
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">176.176.176.0 / 29
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">Interface name here

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 10</h1>
<h5 style="text-align: left;">Firewall/Rules</h5>

Whatever your network name is that's what this is
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NORDVPN_NORDLYNX
<span style="display: inline-block; margin: 0 50px 0 50px">go to the interface that you are going to have this NordVPN go to, and add a rule(s)

Action
 Pass

Interface
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NORDVPN_NORDLYNX
<span style="display: inline-block; margin: 0 50px 0 50px">Interface name here

Protocol
<span style="display: inline-block; margin: 0 50px 0 50px">Any

Source - pick your Alias
<span style="display: inline-block; margin: 0 50px 0 50px">Address or Alias
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">Route_Out_Over_NordVPN_lynx

Destination
<span style="display: inline-block; margin: 0 50px 0 50px">Any

Description
<span style="display: inline-block; margin: 0 50px 0 50px">Allow only VLAN/Network IP's to be routed over NordVPN lynx

<h3 style="text-align: left;">Advanced Options</h3>

Tag
<span style="display: inline-block; margin: 0 50px 0 50px">NordVPN_WG_Kill_Switch_Tag
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">This Tag is the same as Step 11 Tagged text. You can name this anything just make sure that you have it the same as Step 11

Tagged
<span style="display: inline-block; margin: 0 50px 0 50px">empty

State Type
<span style="display: inline-block; margin: 0 50px 0 50px">Keep

Gateway
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NordVPN_nordlynxGW - 10.5.0.2

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 11</h1>
<h5 style="text-align: left;">Firewall/Rules/Floating</h5>

Create / Add a new Floating

Action
<span style="display: inline-block; margin: 0 50px 0 50px">Block

 Interface
<span style="display: inline-block; margin: 0 50px 0 50px"> WAN

Direction
<span style="display: inline-block; margin: 0 50px 0 50px">out
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">if you are going to use gateway under Advanced Options nordvpn then this should be out, if you are going to use gateway default then this can be any
Protocol
<span style="display: inline-block; margin: 0 50px 0 50px">Any

<h3 style="text-align: left;">Source</h3>
Source - pick your Alias
<span style="display: inline-block; margin: 0 50px 0 50px">Address or Alias
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">Route_Out_Over_NordVPN_lynx
Destination
<span style="display: inline-block; margin: 0 50px 0 50px">Any

Description
<span style="display: inline-block; margin: 0 50px 0 50px">Route only via NordVPN lynx

<h3 style="text-align: left;">Advanced Options</h3>

Tag
<span style="display: inline-block; margin: 0 50px 0 50px">Leave empty

Tagged
<span style="display: inline-block; margin: 0 50px 0 50px">NordVPN_WG_Kill_Switch_Tag
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">This Tagged is the same as Step 10 Tag text. You can name this anything just make sure that you have it the same as Step 10 

State Type
<span style="display: inline-block; margin: 0 50px 0 50px">Keep

Gateway
<span style="display: inline-block; margin: 0 50px 0 50px">WG_NordVPN_nordlynxGW - 10.5.0.2
<span style="display: inline-block; margin: 0 50px 0 50px"><span style="display: inline-block; margin: 0 50px 0 50px">If this is default then you can use Direction any, but if you want to use WG_NordVPN then you will have to use a Direction In/Out
<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>