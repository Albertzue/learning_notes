#### There are 3 valid traffic mirrorendpoints: 
      NetworkInterface
      NetworkLoad Balancer
      Gateway Load Balancerendpoints

**Transit Gateway** Network Manager provides a centralized view of global networks built on AWS Transit Gateway. It also
provides the capability to monitor the routing tablesassociated with the transit gateway,and then forward routing information
to CloudWatch Logs Insights. Once in CloudWatch Logs Insights, you can use EventBridge rules to trigger notifications based on
routing changes.

      self signed certsare not supported for Cloud Front
      Incorrect as ACM doesnot support Certificate export, ACM is not supported on EC2
      Incorrect as self signed certsare not supported for Cloud Front.

#### DX:
AS_PATH prepending isa standard BGP way of influencing return traffic for advertised prefixesand SDWAN
supports this

7224:7300 has the highest priority whilst 7224:7100 has the lowest

7224:7XXX BGP communitiesare used for private/transit vifs and 7224:9XXX BGP communitiesare used for public vifs

One DxGW can connect to up to 6 TGW in different accountsand regions.SiteLink will enable the on-prem DC's to communicate via DxGW and the underlying DX connection.

You cannot attach a Direct Connect gateway to a transit gateway when the Direct Connect gateway is already associated with a virtual private gateway or is attached to a private virtual interface

Direct Connect hosted connections only support 1 VIF per connection

### Transit Gateway(TGW):
VXLAN is not supported with TGW

TGW Connect is setup with GRE and BGP

Multicast is a connectionless UDP-based transport,and dynamic group membership is through IGMP

Enabling transit gatewayappliance mode on the VPC attachment in the shared VPC is the solution that requires the least
management overhead and directlyaddresses the issue of dropped traffic between Availability Zones.

Peering TGW will ensure VPC's in the 2 AWS regions connect.

Acceleration is only supported forSite-to-Site VPN connections that are attached to a transit gateway. Virtual private gateways do not support accelerated VPN connections.

#### PrivateLink endpoint:
You cannot create a service endpoint for an ALB. Endpoint services require either a NetworkLoad Balancer or a Gateway Load Balancer 

#### Site-to-Site VPN：
A Site-to-Site VPN connection cannot support both IPv4 and IPv6 traffic simultaneously. The inner encapsulated packets can be either IPv6 or IPv4, but not both. You need separate Site-to-Site VPN connections to transport IPv4 and IPv6 packets

#### ELB:
Perfect Forward Secrecy is a feature that providesadditional safeguardsagainst the eavesdropping of encrypted data, through
the use of a unique random session key.This prevents the decoding of captured data,even if the secret long-term key is
compromised.

### EKS:
we cannot filter VPC flow logs based on EKS worker nodes , but we can create VPC flow logs based on subnetsas resource

### 

### NAT:
      If a connection that's using a NAT gateway is idle for 350 seconds or more, the connection times out.
      
      To prevent the connection from being dropped, you can initiate more traffic over the connection. Alternatively, you can enable
      TCP keepalive on the instance with a value less than 350 seconds
