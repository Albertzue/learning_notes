flow logs does not capture the DNS query itself

      When you create a VPC endpoint to an AWS service, you can enable private DNS. When enabled, the setting createsan AWS
      managed Route 53 private hosted zone (PHZ) which enables the resolution of public AWS service endpoint to the private IP of
      the interface endpoint.The managed PHZ only works within the VPC with the interface endpoint.
      In our setup, when we want spoke VPCs to be able to resolve VPC endpoint DNS hosted in a centralized VPC, the managed PHZ
      won’t work.
      To overcome this, disable the option that automatically creates the private DNS when an interface endpoint is created. Next,
      manually create a Route 53 PHZ and add an Alias record with the full AWS service endpoint name pointing to the interface
      endpoint,as shown in the following figure.



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

The higher the LOCAL_PREF value, the more preferred the route is

You can configure Bidirectional Forwarding Detection (BFD) on your network. Asynchronous BFD isautomaticallyenabled for
each AWS Direct Connect virtual interface. It'sautomaticallyenabled for Direct Connect virtual interfaces, but does not take
effect until you configure it on your router.

private vif and transit vif are both support sitelink

you cannot add iPv6 to an existing s2s and a s2s cannot be dual stack

### Transit Gateway(TGW):
VXLAN is not supported with TGW

TGW Connect is setup with GRE and BGP

Multicast is a connectionless UDP-based transport,and dynamic group membership is through IGMP

Enabling transit gatewayappliance mode on the VPC attachment in the shared VPC is the solution that requires the least
management overhead and directlyaddresses the issue of dropped traffic between Availability Zones.

Peering TGW will ensure VPC's in the 2 AWS regions connect.

Acceleration is only supported forSite-to-Site VPN connections that are attached to a transit gateway. Virtual private gateways do not support accelerated VPN connections.

Accelerated site-to-site VPN isavailable only with TGW VPN attachment, where you can enable it, but you do not manage or
even view the accelerators.

VPC peering has no bandwidth limit unlike Transit Gateway (50Gb/s per VPC attachment)

AWS Transit Gateway Network Manager Route Analyzer, which is designed for analyzing routes in a transit
gateway network, not within a single VPC

#### PrivateLink endpoint:
You cannot create a service endpoint for an ALB. Endpoint services require either a NetworkLoad Balancer or a Gateway Load Balancer 

#### Site-to-Site VPN：
A Site-to-Site VPN connection cannot support both IPv4 and IPv6 traffic simultaneously. The inner encapsulated packets can be either IPv6 or IPv4, but not both. You need separate Site-to-Site VPN connections to transport IPv4 and IPv6 packets

#### ELB:
Perfect Forward Secrecy is a feature that providesadditional safeguardsagainst the eavesdropping of encrypted data, through
the use of a unique random session key.This prevents the decoding of captured data,even if the secret long-term key is
compromised.

Access logs isan optional feature of Elastic Load Balancing that is disabled by default. After you enable access logs for your
load balancer,Elastic Load Balancing captures the logs and stores them in the Amazon S3 bucket that you specify as
compressed files. You can disable access logs at any time. ELB can only send access logs to S3; from there use Athena for querying.

If you need to passencrypted traffic to targets without the load balancer decrypting it, you can create a NetworkLoad Balancer
or Classic Load Balancer with a TCP listener on port 443

### EKS:
we cannot filter VPC flow logs based on EKS worker nodes , but we can create VPC flow logs based on subnetsas resource

### Route53：
Enabling the "fail open" feature in the Route 53 Resolver DNS Firewall VPC configuration ensures that if DNS
Firewall becomes unresponsive, DNS queries will still be resolved.

Single PHZ can be associated with VPCsacross regions.

Route 53 manages the ZSK automatically.The user only needs to manage the KSK (key-signing key).There is no need to explicitly request a ZSK.
DNSSEC worksat the zone level. A DS record isadded to the parent zone, not foreach subdomain, to create the chain of trust

### NAT:
      If a connection that's using a NAT gateway is idle for 350 seconds or more, the connection times out.
      
      To prevent the connection from being dropped, you can initiate more traffic over the connection. Alternatively, you can enable
      TCP keepalive on the instance with a value less than 350 seconds

### Network firewall:
An EXTERNAL_NET rule is a predefined variable in AWS Network Firewall's stateful Suricata-compatible rules that represents all IP addresses outside of your specified HOME_NET. Network Firewall uses HOME_NET to define your private or trusted networks and EXTERNAL_NET to represent all other public IP addresses. Rules using EXTERNAL_NET as a source or destination allow or block traffic from or to the public internet or other external networks. 
