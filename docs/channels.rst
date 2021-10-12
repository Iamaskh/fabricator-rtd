##################
Channel Creation & Joining
##################


This is a basic tutorial on creating and joining on a channel. 

.. note::

    This tutorial currently demonstrates an example of 3 organizations. However the same steps shall be followed for up to *N organizations*.


Organization 1
##############

To create a channel run following command. This commands creates the channel from the anchor peer i.e.  of *oganization 1* and also make it join this new channel.

.. code-block:: bash
    
    $ ./fabric-network.sh create-channel ChannelAll channelall

 
Organization 2
##############
To Add Org 2 configuration in the channel copy Org2.json file in channel-artifacts folder of Org1 and run following commands.
Usually add-org-config and add-org-sign are supposed to run from 2 different Orgs (depending upon channel configuration in configtx.yaml), but in this case since we only have Org1 currently added in this channel we can make an exception and add & sign both from Org1.
But it would not be possible if there are more than 1 Orgs on a particular channel.

.. code-block:: bash
    
	$ ./fabric-network.sh add-org-config channelall Org2
	
    	$ ./fabric-network.sh add-org-sign channelall Org2

The channel channelall has been updated with the new organization and new genesis block is now added in ./channel-artifacts/channelall.block file
Copy this file ./channel-artifacts/channelall.block in new organization's channel-artifacts and join this channel from Org2

To join a channel by anchor peer i.e. peer0 of Org2 whose configuration is already added and signed, copy .block file from Org1 in channel-artifacts folder and run the following command.
You can run this command for each peer of Org2 to join the channel by changing peer in the argument.

.. code-block:: bash
    
    $ ./fabric-network.sh join-channel peer0 channelall


Organization 3
##############

To Add Org 3 configuration in the channel copy Org3.json file in channel-artifacts folder of Org2 and run following commands.
Now add-org-config and add-org-sign would from 2 different Orgs (depending upon channel configuration in configtx.yaml), as now there are more than 2 Orgs on channelall.

.. code-block:: bash
    
    $ ./fabric-network.sh add-org-config channelall Org3


(1) The new organization configuration for this channel is exported in channel-artifacts/Org3_update_in_envelope.pb file
(2) Copy channel-artifacts/Org3_update_in_envelope.pb file in channel-artifacts folder of any other Org in this channel i.e. Org1
(3) run ./fabric-network add-org-sign from any other organization on this channel to sign this configuration and commit to ledger i.e. Org1

To Sign Org 3 configuration added by Org2 in step 5, copy channel-artifacts/Org3_update_in_envelope.pb file in channel-artifacts and run following command

.. code-block:: bash
    
    $ ./fabric-network.sh add-org-sign channelall Org3

The channel channelall has been updated with the new organization and new genesis block is now added in ./channel-artifacts/channelall.block file
Copy this file ./channel-artifacts/channelall.block in new organization's channel-artifacts and join this channel from anchor peer cli.

To join a channel by anchor peer i.e. peer0 of Org3 whose configuration is already added and signed, copy .block file from Org1 in channel-artifacts folder and run the following command.
You can run this command for each peer of Org3 to join the channel by changing peer in the argument.

.. code-block:: bash
    
    $ ./fabric-network.sh join-channel peer0 channelall
