# Add Interfaces to an Existing Template

The prior step creates a new template. This stage is the complement to
complete template configuration adding topology-specific interfaces.

## Workflow Skillet

Defines the skillet stages for adding interfaces to the template.

It also includes the logic decision for SD-WAN or non SD-WAN interface configuration.
SD-WAN configuration requires additional elements to enable SD-WAN on physical interface,
setup a next-hop gateway, and create the SD-WAN interface.

## Get Template List

A rest skillet that queries Panorama to get a list of configured templates.
The user can then select which template is to be used for adding interfaces.

In PanHandler, ```Show Capture Values``` can be selected when the skillet is
run to see and validate the list returned from Panorama.

## Get Zone, Virtual Router, and Interface Profile Lists

Once the template is selected the next REST skillet will again query Panorama
to get a list of zones, virtual routers and interface profiles to be used
as dropdown inputs for the specific interface configuration.

In PanHandler, ```Show Capture Values``` can be selected when the skillet is
run to see and validate the list returned from Panorama.

## Add Interface to Template - SD-WAN Enabled

Based on the workflow selection, this skillet is run if the interface is
an SD-WAN interface. Along with physical interface configuration SD-WAN are 
also added.

Key elements for the interface:

* Physical interface name and ip address type (static or DHCP)
* For static interfaces, set up Panorama variables for the ip address and next-hop gateway
* For DHCP interfaces disable the DHCP default route
* Associate zones and virtual routing to the interface
* Create the SD-WAN interface and associate an interface profile

## Add Interface to Template - no SD-WAN

A simplified skillet that excludes the SD-WAN configuration elements. It only
configures:

* Physical interface name and ip address type (static or DHCP)
* For static interfaces, set up Panorama variables for the ip address only
* Associate zones and virtual routing to the interface

## Workflow Complete Summary Output

This is a simple text render to screen to show the user a configuration
summary and that this workflow is complete.