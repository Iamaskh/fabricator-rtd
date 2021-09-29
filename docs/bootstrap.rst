Bootstrap
=====

The bootstrap process brings up the required containers for each organization. This bootstrap process for local setup is already done in local-startup.sh script. For bootstrapping network with organizations on separate machines, we have a script remote-startup.sh.

You can run the script remote-startup.sh from a single machine (Org1) after you have generated-org for each organization on individual machines. Please update the variables at the top of remote-startup.sh with appropriate endpoints for each organization's machine.

Run the below command from Org1 in order to run basic network with 3 organizations.

.. code-block:: bash

    	$ ./remote-startup.sh bootstrap

Once 3 organizations have been bootstrapped then we can create and join the channels in which these organizations can participate. We have added hardcoded profiles ChannelAll, ChannelAll2, ChannelAllANY in configtx.yaml files of organizations respectively and these channels can be created from their respective organizations and subsequently be joined by other organizations. In simple steps as demonstrated below.

.. code-block:: bash

        $ ./remote-startup.sh create-join-channel channelall

        $ ./remote-startup.sh create-join-channel channelall2
	    
        $ ./remote-startup.sh create-join-channel channelallany


As explained previously: channelall, channel2 => Majority organizations need to sign channelallany => ANY organization needs to sign

At this point, you have achieved to create a remote network with 3 organizations joined by two channels.

If you want to do all these steps manually which are inside remote-startup.sh, the commands are explained below.

For the basic tutorial on setting up 3 organizations, use the following commands:

This series of commands is an interactive process between the organizations so please follow the instructions in the sequence in which they are numbered.

Organization 1
###########

To read all the help regarding commands use: ./fabric-network.sh help

To start


.. code-block:: bash

        $ ./fabric-network.sh generate-crypto

	$ ./fabric-network.sh up

To bootstrap Org2 from Org1


.. code-block:: bash

        $ ./fabric-network.sh add-remote-orderer 10

        In above command 10 refers to orderer number. Since we are bootstrapping Org2's base orderer it is 10, it should be 20 for Org3 and so on..
	As a result of this command for base orderer10 a genesis file will be generated in channel-artifacts folder i.e. channel-artifacts/orderer_genesis.pb
	Next step: Copy the channel-artifacts/orderer_genesis.pb into channel-artifacts/orderer_genesis.pb of the Org2 

        $ ./fabric-network.sh publish-remote-orderer 10

	    
        The above command ensures that the base orderer of Org2 is published and now peers can contact this as an active orderer in the network. 
	This command must be run after the containers of Org2 are up and running

Organization 2
###########

To start bootstraping Org2, Copy the shared orderer certificates (OrdererSharedCerts folder) from first organization's channel-artifact folder in Org2 i.e. Org2/OrdererSharedCerts. Once the shared certificates are placed as required run following commands.