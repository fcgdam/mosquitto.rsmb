RSMB changes
============

What are the changes on this repository regarding the parent/original repository?

# Hop extension for advertisement packets

On the original repository, the advertise directive for the MQTT-SN protocol doesn't specify a hop limit for the advertisement packets.
By default that value is 1, which means that those packets can't transverse some network elements like for example routers.

On this repository, a 4th parameter is available, where the hop limit for the advertise packet can be specified to a value different of 1.

An example:

'''
advertise FF04::123:1884 10 33 5
'''

This directive specifies that each 10 seconds, an advertisement packet with gateway id of 33 is broadcasted to multicast address of FF04::123 port 1884 with an hop limit of 5.
If the parameter is not specified, the default/original value of 1 is used.

# SEARCHGW packet support

On the original repository, support for SEARCHGW MQTT-SN packet is not available. This repository supports SEARCHGW packets by responding to them with a GWINFO MQTT-SN packet.
Since the SEARCHGW packets are sent on a multicast address, the response should also be sent on a multicast address since it is expected that nodes will be listening to a multicast address.

A non backward compatible directive exists on this repository that allows to send a GWINFO packet response with the gateway id. Nodes can obtain the gateway/broker address from the source address and port. If the directive is not specified the behavior is as the original repository, no action for SEARCHGW packets.

'''
gwinfo FF04::123:1884 12 5
'''

This directive enables response to a SEARCHGW packet where a GWINFO packet response is sent to the FF04::123:1884 multicast group with gateway id 12, and a packet hop limit of 5.

# Limitations and warnings

While these changes work, the testing is/was pretty limited, and hence this repository should be treated as a proof of concept without any warranties of fit for purpose of any kind. Use on own risk and only for testing. If in doubt use the original repository.

Again: USE AT YOUR OWN RISK. The user bears sole risk for use.

