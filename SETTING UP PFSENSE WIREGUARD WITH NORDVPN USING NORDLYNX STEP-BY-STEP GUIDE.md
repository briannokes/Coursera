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
<span style="display: inline-block; margin: 0 50px 0 50px">PrivateKey -	Your Private Key info here</span>
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

 Endpoint
 
	 The Hostname will change when you need a new server

Hostname
usXXXX.nordvpn.com 

When you see XXXX you need these numbers from nordvpn website server and find what is best but for now, if you want you can use this one for " us8258.nordvpn.com ', and you can use this one for " uk1818.nordvpn.com " "usXXXX.nordvpn.com" - change the XXXX to any number that NordVPN has that you get when you log in from Windows or Linux you should see these numbers and then you can just change the number part if you are using us = USA or here is a sample UK one - uk1818.nordvpn.com

Port

	51820

 Public Key - From nordvpn peer content
 
	Public Key

Public Key from NordVPN peer content here 

	 Pre-shared Key - Leave blank - optional
	 
	NA - no Generate

<h3 style="text-align: left;"></h3>  Address Configuration

Allowed IPs 
	0.0.0.0 / 0

Description
	us8258.nordvpn.com:51820
		When you see XXXX you need these numbers from nordvpn website server and find what is best but for now, if you want you can use this one for " us8258.nordvpn.com ', and you can use this one for " uk1818.nordvpn.com " usXXXX.nordvpn.com:51820 - change the XXXX to any number that NordVPN has that you get when you log in from Windows or Linux you should see these numbers and then you can just change the number part if you are using us = USA or here is a sample UK one - uk1818.nordvpn.com
<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>
<h1 style="text-align: left;">Step 4</h1>
<h3 style="text-align: left;">System/Routing/Gateways</h3>

now create your Gateway for nordvpn

Interface
	WG_NORDVPN_NORDLYNX

 Name
	 WG_NordVPN_nordlynxGW

 Gateway
	 10.5.0.2

 Description
	 WireGuard-Nordvpn lynx

Monitor IP
	8.8.8.8 or any other IP to see connection in Status / Dashboard widgets name Gateways us this to see Status Online or when its off or not working

Description
	WireGuard-Nordvpn lynx

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>
<h1 style="text-align: left;"></h1> Step 5
When putting it on a VLAN or network
<h5 style="text-align: left;"></h5>Firewall/NAT/Outbound
	Mappings
	
Create / Add a new one
	Edit Advanced Outbound NAT Entry
	
Interface
	WG_NORDVPN_NORDLYNX

Protocol
	Any

Source
	Type
		Network or Alias
			176.176.176.0/29

Destination
	Type
		Any

<h2 style="text-align: left;"></h2>  Translation

Address
	WG_NORDVPN_NORDLYNX address

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;"></h1> Step 6
<h5 style="text-align: left;"></h5>Firewall/Rules
	WAN

Action
	Pass

Interface
	WAN

Protocol
	UDP

<h3 style="text-align: left;"></h3>  Source
Source
	Any

<h3 style="text-align: left;"></h3>  Destination
Destination
	WG_NORDVPN_NORDLYNX address
		This is your interface that you created for the NordVPN WireGuard

Destination Port Range
	 From
		 Other
	Custom
		51820
	To
		Other
	Custom
		51820

Description
	Allow WireGuard - 51820

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 7</h1>

<h5 style="text-align: left;"></h5>Firewall/Rules
	WG_NORDVPN_NORDLYNX
Create / Add new Rule

<h3 style="text-align: left;"></h3>  Edit Firewall Rule

Action
	Pass

Interface
	WG_NORDVPN_NORDLYNX

Protocol
	Any
<h3 style="text-align: left;"></h3>  Source
Source
	Any
<h3 style="text-align: left;"></h3>  Destination
Destination
	Any

Description
	Allow All Traffic for WG VPN

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 8</h1>
<h5 style="text-align: left;">Firewall/Rules</h5>
	WireGuard

Action
	Pass

Interface
	WireGuard

Address Family
	IPv4

Protocol
	Any
<h3 style="text-align: left;"></h3>  Source
Source
	Any
<h3 style="text-align: left;"></h3>  Destination
Destination
	Any

Description
	Pass VPN traffic from WireGuard peers

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 9</h1>
<h5 style="text-align: left;">Firewall/Aliases</h5>

Create / Add new Aliases

Name
	Route_Out_Over_NordVPN_lynx

Description
	Route_Out_Over_NordVPN_lynx

Type
	Network(s)
		Network or FQDN - You can add this to however many networks you need to add this VPN to. I am just using this one VLAN network I created in this example.
			176.176.176.0 / 29
				Interface name here

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 10</h1>
<h5 style="text-align: left;">Firewall/Rules</h5>

Whatever your network name is that's what this is
	WG_NORDVPN_NORDLYNX
	go to the interface that you are going to have this NordVPN go to, and add a rule(s)

Action
 Pass

Interface
	WG_NORDVPN_NORDLYNX
	Interface name here

Protocol
	Any

Source - pick your Alias
	Address or Alias
		Route_Out_Over_NordVPN_lynx

Destination
	Any

Description
	Allow only VLAN/Network IP's to be routed over NordVPN lynx

<h3 style="text-align: left;">Advanced Options</h3>

Tag
	NordVPN_WG_Kill_Switch_Tag
		This Tag is the same as Step 11 Tagged text. You can name this anything just make sure that you have it the same as Step 11

Tagged
	empty

State Type
	Keep

Gateway
	WG_NordVPN_nordlynxGW - 10.5.0.2

<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>

<h1 style="text-align: left;">Step 11</h1>
<h5 style="text-align: left;">Firewall/Rules/Floating</h5>

Create / Add a new Floating

Action
	Block

 Interface
	 WAN

Direction
	out
		if you are going to use gateway under Advanced Options nordvpn then this should be out, if you are going to use gateway default then this can be any
Protocol
	Any

<h3 style="text-align: left;">Source</h3>
Source - pick your Alias
	Address or Alias
		Route_Out_Over_NordVPN_lynx
Destination
	Any

Description
	Route only via NordVPN lynx

<h3 style="text-align: left;">Advanced Options</h3>

Tag
	Leave empty

Tagged
	NordVPN_WG_Kill_Switch_Tag
		This Tagged is the same as Step 10 Tag text. You can name this anything just make sure that you have it the same as Step 10 

State Type
	Keep

Gateway
	WG_NordVPN_nordlynxGW - 10.5.0.2
		If this is default then you can use Direction any, but if you want to use WG_NordVPN then you will have to use a Direction In/Out
<h2 style="text-align: left;">Save</h2>
<br>
<span style="display:block; background-color:red; width:100%; height:2px;"></span>