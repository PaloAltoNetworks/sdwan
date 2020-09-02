# Assign Device to Device-Group and Template Stack

Step 0 onboarding devices to Panorama for basic operational tasks
such as licensing, software updates, and content updates.

After the devices are onboarding, updates, and site-type template stacks
and device-groups have been created then the devices can be assigned to their
respective stacks and device-groups.

## Workflow Skillet

Defines the skillet stages for assigning devices to stacks and device-groups.

## Get Device, Template-Stack, and Device-Group Lists

A rest skillet that queries Panorama to get a list of onboarded devices,
template-stacks, and device-groups.

In PanHandler, ```Show Capture Values``` can be selected when the skillet is
run to see and validate the list returned from Panorama.

## Add Device to Template-Stack and Device-Group

This is a simple association skillet where the user selects the device
serial-number, a stack, and device-group. The device is then assigned to 
these elements in Panorama.

## Get List of Panorama Variables (Optional)

If the device is associated to a template-stack with Panorama variables, a
list of the variables names is captured to be used by the next step.

In PanHandler, ```Show Capture Values``` can be selected when the skillet is
run to see and validate the list returned from Panorama.

## Configure Panorama Variable Values

For static interfaces, the user is provided with a list of variables for
the selected template and values are entered. These values are associated to
the specific device when onboarded and the configuration is pushed from
Panorama to the device.

The use of variables allows for multiple devices to be associated to the same
template but with varying interface addresses and next-hop gateways.

## Workflow Complete Summary Output

This is a simple text render to screen to show the user a configuration
summary and that this workflow is complete.