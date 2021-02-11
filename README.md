# SD-WAN Configuration Skillets

## Tested with Panorama 10.0.3, SD-WAN plugin 2.0.2, and  PAN-OS 10.0.3

This is a set of modular skillets for Panorama and the SD-WAN plugin

The set of skillets do not provide a panorama day 1, upgrade software, 
or install and activate the plugin.

Each step uses a workflow skillet model to guide the user, query panorama
to provide valid configuration options, and give a step summary at the end.

### Optional Step to include IronSkillet

This will load the shared device-group and template configuration for the
IronSkillet day one best practice baseline.

In step 2 below when adding a new site, if the user opts to include
IronSkillet, the newly created template-stack will include the
iron-skillet template.

This is useful to inherit the security elements such as device hardening
and recommended security profiles/groups.

### Step 0 - Device Onboarding

Preliminary step to configure Panorama with device serial numbers. One or more
devices can be onboarded during this step.

After devices are configured with the Panorama IP they will connect without
any template stack or device-group association. During this step the intent
is to upgrade software, install content updates, and license the devices.

### Step 1 - Configure Shared Elements

Add the following shared elements to Panorama:

* recommended link tags
* application group to be used in policies
* catch-all traffic distribution and path quality profiles
* catch-all sdwan post rule for unmatched sessions
* application pre-rule for bgp traffic including an sdwan logging profile
* recommended traffic distribution profiles
* reference interface profiles and template
* SD-WAN VPN Address Pool

### Step 2 - Add New Site

Configure template, stack, and device-group for a new hub or branch site.

Includes the following configuration elements:

* add device-group with a sample SD-WAN policy rule
* add template with interface profiles and predefined zones
* add template stack including site-specific template
* include a virtual-router instance
* select to include ironSkillet as part of the template-stack

The template created is topology agnostic. The next step will add interfaces
to become topology specific based on interface requirements.

NOTE: add new templates as required to match topology variation such as
number of interfaces and interface types.

### Step 3 - Add Interface to Template

The previous step creates a site template foundation and this step then adds
each required interface based on the topology.

Topology variation for this skillet is based on the PHY interface type.
If static the user will be prompted for panorama variable name assignment for the
interface and next-hop gateway addresses. If a dhcp interface, no panorama
variables are used.

When the device is assigned to its template-stack and respective template,
the user will then input the values for the associated panorama variables 
if the template uses static interfaces.

The user can choose if the added interface is sd-wan enabled or just a
standard interface. If sd-wan enabled, then the sd-wan virtual interface
and associated configuration will be included.

Configuration elements in this step include:

* physical ethernet interface attributes
* enable SD-WAN on the phy interface
* assign an SD-WAN interface profile to the phy interface
* zone and virtual-router assignment for the interface
* create panorama variables for static interface ip address and gateway

This is step is repeated for each interface to be added to the site template.

This workflow includes 2 rest type skillets to query Panorama and generate
a set of pulldown list options for:

* template selection
* zone names
* virtual-router names
* interface profile names

### Step 4 - Assign Device to Device-Group and Template-Stack

Assign an already onboarded and licensed device to a device-group and 
template-stack based on the device's role in the topology. The device MUST
be assigned to a template with matching physical interface requirements.

If the template includes Panorama variables, a list of variables will be
presented allowing the user input the device-specific values.

Repeat this step for each device to be assigned to a device-group and
template-stack. Currently the skillet only supports assigned of a single
device. Bulk loading can be done using csv import.

### Step 5 - Onboard Device to SD-WAN Plug-In

The device is mapped into the SD-WAN topology using the following elements:

* SD-WAN type: hub or branch
* virtual-router name
* site description
* (Optional) BGP routing configuration

Repeat this step for each device to be included in the SD-WAN topology.
Currently the skillet only supports single device onboarding. Bulk loading
can be done using csv import.

### Next Steps

* Use the Panorama GUI to create the vpn cluster
* configure security policies to map application usage for SD-WAN
* push the configuration to the devices and validate a successful commit
