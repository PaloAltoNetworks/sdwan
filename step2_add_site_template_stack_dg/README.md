# Add a New SD-WAN Site Workflow

Configures a skeleton template and followed by the next workflow stage
to add interfaces to the template based on topology requirements.

## Workflow Skillet

Basic workflow with stages to add the shared elements and then display
end of workflow output text.

## Configure a Hub or Spoke Template with Shared Elements

Create a named hub or spoke template and add shared device-group configuration.

Shared elements include:

#### recommended link tags

These are used by SD-WAN to map interface types for SD-WAN routing. The
day one configuration adds:

* Low Cost Paths
* Expensive Paths
* General Access

This is a reference list that may be updated as best practices emerge.
Users can also include their own link tags for custom configuration.

#### application group to be used in policies
This is a reference application group example. Users can build on this group
and add their own. This simplifies mapping sets of applications to their respective
traffic-profile based policies.

#### catch-all traffic distribution and path quality profiles
The equivalent of best-effort routing, these profiles are added with
sub-optimal metrics to avoid conflict with preferred SD-WAN interfaces

The catch-all ensures that there is always a match criteria for applications.

#### catch-all sdwan post rule for unmatched sessions

This SD-WAN post rule uses the catch-all profiles to ensure applications are
handled properly by SD-WAN when not matching other policy rules.

This equates to best-effort traffic management.

#### application pre-rule for bgp traffic and sdwan logging profile
These rules are used to ensure BGP routing traffic is allowed between
hub and branch sites.

Actions include allow with security-mapping to default security profiles
such as AV, anti-spyware, and Wildfire. Also included is a logging profile
called ```sdwan``` to capture traffic and threat information related to
the bgp policy.

#### recommended traffic distribution profiles
The initial release of the skillet includes the traffic distribution profile
``` least expensive link first```. Additional recommended profiles will be
added based on user demand.

This is used in the SD-WAN policy sample pre-rule.


#### reference interface profiles and template

The reference template is used to

* be an example that could be cloned for custom templates
* required for the Panorama API to add device-group shared elements

It includes the following configuration elements also used by the
Step 2 'Add a New Site' template configuration

* predefined zones: zone-to-branch, zone-to-hub, zone-internal, zone-internet
* zones to be used for physical interface associations: wan, lan
* interface profiles for Ethernet, ADSL, and LTE

## Workflow Complete Summary Output

This is a simple text render to screen to show the user a configuration
summary and that this workflow is complete.