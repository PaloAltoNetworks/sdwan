# Onboard Device to SD-WAN

Step 0 onboarding devices to Panorama for basic operational tasks
such as licensing, software updates, and content updates. In Step 4
they are assigned to their template-stacks and device-groups.

This skillet step brings them under control of the SD-WAN plug-in by
defining them as hub or branch and optionally setting up BGP routing.

## Workflow Skillet

Defines the skillet stages for assigning devices to stacks and device-groups.

## Get Device List

A rest skillet that queries Panorama to get a list of onboarded devices.

In PanHandler, ```Show Capture Values``` can be selected when the skillet is
run to see and validate the list returned from Panorama.

## Add Device to SD-WAN

Devices are added to SD-WAN including

* hub or spoke designation
* site name
* virtual router name
* BGP router-id, loopback address, AS and route to be redistributed


## Workflow Complete Summary Output

This is a simple text render to screen to show the user a configuration
summary and that this workflow is complete.