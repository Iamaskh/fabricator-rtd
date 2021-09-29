Channel Creation & Joining
=====

For the basic tutorial on creating and joining on a channel use the following commands:

Please follow the instructions in the sequence in which they are numbered.

Organization 1
##############

To create a channel run following command. This commands creates the channel from achor peer i.e. peer0 and also join it this new channel.



.. code-block:: bash
    
    $ ./fabric-network.sh create-channel ChannelAll channelall


To Add Org 2 configuration in the channel copy Org2.json file in channel-artifacts folder of Org1 and run following commands. Usually add-org-config and add-org-sign are supposed to run from 2 different Orgs (depending upon channel configuration in configtx.yaml), but in this case since we only have Org1 currently added in this channel we can make an exception and add & sign both from Org1. But it would not be possible if there are more than 1 Orgs on a particular channel.



.. code-block:: bash

    $ ./fabric-network.sh add-org-config channelall Org2
	$ ./fabric-network.sh add-org-sign channelall Org2

	The channel channelall has been updated with the new organization and new genesis block is now added in ./channel-artifacts/channelall.block file
	Copy this file ./channel-artifacts/channelall.block in new organization's channel-artifacts and join this channel from Org2

To Sign Org 3 configuration added by Org2 in step 5, copy channel-artifacts/Org3_update_in_envelope.pb file in channel-artifacts and run following command


.. code-block:: bash

        $ ./fabric-network.sh generate-crypto

        This command generates 2 important files for bootstrapping
	(1) A json file i.e. ./channel-artifacts/Org2.json that contains the Org2 MSP certificates required to join this Org to any channel at any time
	(2) A crt file i.e. ./channel-artifacts/orderer10.crt that contains public certificates of Org2's base orderer required to add this base orderer into system channel to bootstrap
	As a next step copy the ./channel-artifacts/orderer10.crt into channel-artifacts folder of Org1 so that it can bootstrap Org2's base orderer in system channel



In step 4 a genesis file would have been generated in Org1/channel-artifacts/orderer_genesis.pb copy this file to Org2/channel-artifacts/orderer_genesis.pb and then run the following command to start the containers 5. ./fabric-network.sh up

After the containers of Org2 are up, publish it's orderer details by running the command in step 6.

To Bootstrap Org3 from Org2

.. code-block:: bash

    $ ./fabric-network.sh add-org-sign channelall Org3

	The channel channelall has been updated with the new organization and new genesis block is now added in ./channel-artifacts/channelall.block file
	Copy this file ./channel-artifacts/channelall.block in new organization's channel-artifacts and join this channel from anchor peer cli


 
Organization 2
##############

To join a channel by anchor peer i.e. peer0 of Org2 whose configuration is already added and signed, copy .block file from Org1 in channel-artifacts folder and run the following command. You can run this command for each peer of Org2 to join the channel by changing peer in the argument.

.. code-block:: bash

	$ ./fabric-network.sh join-channel peer0 channelall

To Add Org 3 configuration in the channel copy Org3.json file in channel-artifacts folder of Org2 and run following commands. Now add-org-config and add-org-sign would from 2 different Orgs (depending upon channel configuration in configtx.yaml), as now there are more than 2 Orgs on channelall.

.. code-block:: bash

    $ ./fabric-network.sh add-org-config channelall Org3

	(1) The new organization configuration for this channel is exported in channel-artifacts/Org3_update_in_envelope.pb file
	(2) Copy channel-artifacts/Org3_update_in_envelope.pb file in channel-artifacts folder of any other Org in this channel i.e. Org1
	(3) run ./fabric-network add-org-sign from any other organization on this channel to sign this configuration and commit to ledger i.e. Org1

Organization 3
##############

To join a channel by anchor peer i.e. peer0 of Org3 whose configuration is already added and signed, copy .block file from Org1 in channel-artifacts folder and run the following command. You can run this command for each peer of Org3 to join the channel by changing peer in the argument.

.. code-block:: bash

	$ ./fabric-network.sh join-channel peer0 channelall
