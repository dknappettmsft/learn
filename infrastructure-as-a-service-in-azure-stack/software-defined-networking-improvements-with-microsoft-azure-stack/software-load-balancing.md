# Software Load Balancing

The Software Load Balancer Virtual IPs (VIPs) reside on the Software Load Balancer Multiplexer (MUX). This is a service deployed on to multiple Virtual Machines in the Azure Stack environment. It is responsible for converting packets destined for a VIP to a dedicated IP (DIP) behind the Software Load Balancer. As it is a distributed service it relies on two key networking protocols BGP and Equal Cost Multi-Path (ECMP) routing. Using BGP allows for the physical network appliances to do the following:

- Learn where VIPs are available on MUXes, even if the MUXes are on different subnets.

- Balance the load for each VIP across available MUXes buy using ECMP routing.

- Automatically detect failures in the MUX infrastructure to prevent it from sending traffic to a failed MUX. This could be because the Hyper-V host where the MUX is residing has failed, the MUX has been decommissioned, or the MUX is being updated.

This integration of the Software Load Balancer with the Network Controller is critical because the Network Controller is responsible for updating the Hyper-V hosts with information on where the MUXes are located so that the tenant traffic can be routed correctly.

All physical network equipment used with the Azure Stack deployment must be able to utilize the BGP protocol so that the Network Controller can update them accordingly. In addition, the physical network equipment also exchanges information based on the BGP protocol.