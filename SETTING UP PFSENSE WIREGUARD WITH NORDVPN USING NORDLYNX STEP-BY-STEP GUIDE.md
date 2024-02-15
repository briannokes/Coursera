# [[Website Creation - SETTING UP PFSENSE WIREGUARD WITH NORDVPN USING NORDLYNX STEP-BY-STEP GUIDE]]


[Setting Up pfSense WireGuard with NordVPN Using NordLynx Step-by-Step Guide](https://sites.google.com/view/nordvpn-wireguard-pfsense/home)

<h1 style="text-align: center;"># SETTING UP PFSENSE WIREGUARD WITH NORDVPN USING NORDLYNX STEP-BY-STEP GUIDE</h1> 

Thank you for taking the time to explore this comprehensive guide. I've invested significant effort into its creation, aiming to provide you with detailed and valuable insights. I trust that you will find it helpful and worthy of sharing with others.  
  
Created by Brian Robert Nokes

## The first thing In pfSense, is to navigate to the VPN then WireGuard. Then create a Tunnel. 

# Step 1

###### VPN/WireGuard/Tunnels

### Tunnel Configuration - tun_wg0
	Enable Tunnel - check mark on

 Description
	WireGuard-Nordvpn

 Listen Port
	51820

 Interface Keys
	 Private key from NordVPN content which goes into Private key for this tunnel. (Required)
PrivateKey
	Your Private Key info here
## Save

# Step 2

 Interfaces/Interface Assignments
	 Interfaces

create WG_NordVPN_nordlynx (tun_wg0)

#### General Configuration 

Enable - Check mark on

 Description
	WG_NordVPN_nordlynx

 IPv4
	Static IPv4

 IPv4 Address
	10.5.0.2 /32 - pick anything that you don't have or someone else may not or just keep what NordVPN uses

 IPv4 Upstream gateway
	Selecting an upstream gateway causes the firewall to treat this interface as a WAN-type interface. 

This is a WAN-type interface NordVPN WG_NordVPN_nordlynxGW - 10.5.0.2
## Save

# Step 3

###### /VPN/WireGuard/Peers

### Peers Configuration

Enable Peer - check mark on

 Tunnel 
	 tun_wg0

 Description
	 WireGuard-Nordvpn

 Dynamic Endpoint
	 Uncheck this option - to assign NordVPN endpoint address and port for this peer, this needs to be off - no check mark

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

### Address Configuration

Allowed IPs 
	0.0.0.0 / 0

Description
	us8258.nordvpn.com:51820
		When you see XXXX you need these numbers from nordvpn website server and find what is best but for now, if you want you can use this one for " us8258.nordvpn.com ', and you can use this one for " uk1818.nordvpn.com " usXXXX.nordvpn.com:51820 - change the XXXX to any number that NordVPN has that you get when you log in from Windows or Linux you should see these numbers and then you can just change the number part if you are using us = USA or here is a sample UK one - uk1818.nordvpn.com
## Save

# Step 4
###### System / Routing / Gateways 

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

## Save

# Step 5
When putting it on a VLAN or network
###### Firewall/NAT/Outbound
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

## Translation

Address
	WG_NORDVPN_NORDLYNX address

## Save

# Step 6
###### Firewall/Rules
	WAN

Action
	Pass

Interface
	WAN

Protocol
	UDP

### Source
Source
	Any

### Destination
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

## Save

# Step 7

###### Firewall/Rules
	WG_NORDVPN_NORDLYNX
Create / Add new Rule

### Edit Firewall Rule

Action
	Pass

Interface
	WG_NORDVPN_NORDLYNX

Protocol
	Any
### Source
Source
	Any
### Destination
Destination
	Any

Description
	Allow All Traffic for WG VPN

## Save

# Step 8
###### Firewall/Rules
	WireGuard

Action
	Pass

Interface
	WireGuard

Address Family
	IPv4

Protocol
	Any
### Source
Source
	Any
### Destination
Destination
	Any

Description
	Pass VPN traffic from WireGuard peers

## Save

# Step 9
###### Firewall/Aliases

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

## Save

# Step 10
###### Firewall/Rules

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

### Advanced Options

Tag
	NordVPN_WG_Kill_Switch_Tag
		This Tag is the same as Step 11 Tagged text. You can name this anything just make sure that you have it the same as Step 11

Tagged
	empty

State Type
	Keep

Gateway
	WG_NordVPN_nordlynxGW - 10.5.0.2

## Save

# Step 11
###### Firewall/Rules/Floating

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

### Source
Source - pick your Alias
	Address or Alias
		Route_Out_Over_NordVPN_lynx
Destination
	Any

Description
	Route only via NordVPN lynx

### Advanced Options

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
## Save