###########################
Choosing a Device Hierarchy
###########################
When designing a solution that utilizes one, or many, gateways with nodes attached
to that gateway, a decision needs to be made about how to handle the CIKs for
each device.  This page will give an introduction to the topic of choosing
how to store these ciks



Common Hierarchies
------------------
How to structure the hierarcy of the devices in your system typically falls
into one of three different ways.

1. Each node and gateway stores and uses its own cik
2. Each node and gateway has its own cik, but the gateway stores the cik for each node
3. Only the gateway has a cik and it uses 

Which Hierarchy To Choose?
--------------------------
Choosing one of the three methods is a decision that should be made after you
know what type of hardware you will be using, and what type of information you
want to send to One Platform.

Options #1 and #2 both use the same concept of one cik per device, whereas
option #3 uses one CIK per node/gateway group.  The most flexible solution
is a one-to-one relationship between physical devices (nodes/gateway) and
the devices on your platform.  This allow you to add/remove devices as nodes
are updated/replaced, without having to change your data model.  

There are, however, times when you will only want one cik per gateway and all 
of it's nodes.  This may happen when the configuration of nodes/gateways is 
always the same.  For example, your system measures tire pressures on a
motorcycle.  In this instance you know that you will always have a front tire
pressure and a rear tire pressure sensor, and one gateway.  In this case, even
if you swap out sensors, you still have one front pressure sensor and one rear
pressure sensor.

The only difference between options #1 and #2 is the where the CIK is stored.
Often times your sensor node devices may not be able to store their cik on board
or they are already in working systems and you do not want to alter their
firmware/software.  If this is the case you will want to go with option #2.  This
adds more complexity and additional state to the gateway.

Alternatively this complexity and state can be moved to the sensor nodes allow

Other advantages?
