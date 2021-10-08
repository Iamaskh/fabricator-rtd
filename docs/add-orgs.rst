##################
Adding organizations
##################

For the basic tutorial on setting up 3 organizations, use the following commands:

This series of commands is an interactive process between the organizations so please follow the instructions in the sequence in which they are numbered.

Organization 1
##############

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
##############

To start bootstraping Org2, Copy the shared orderer certificates (OrdererSharedCerts folder) from first organization's channel-artifact folder in Org2 i.e. Org2/OrdererSharedCerts. Once the shared certificates are placed as required run following commands.

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

        $ ./fabric-network.sh add-remote-orderer 20

        In above command 20 refers to orderer number. Since we are bootstrapping Org3's base orderer it is 20, it should be 30 for Org4 and so on..
	As a result of this command for base orderer20, a genesis file will be generated in channel-artifacts folder i.e. channel-artifacts/orderer_genesis.pb
	Next step: Copy the channel-artifacts/orderer_genesis.pb into channel-artifacts/orderer_genesis.pb of the Org3 

        $ ./fabric-network.sh publish-remote-orderer 20

	    
        The above command ensures that the base orderer of Org3 is published and now peers can contact this as an active orderer in the network. 
        This command must be run after the containers of Org3 are up and running


Organization 3
##############       

To start bootstraping Org3, Copy the shared orderer certificates (OrdererSharedCerts folder) from first/2nd organization's channel-artifact folder in Org3 i.e. Org3/OrdererSharedCerts. Once the shared certificates are placed as required run following commands.

.. code-block:: bash

      $ ./fabric-network.sh generate-crypto 

	This command generates 2 important files for bootstrapping
	(1) A json file i.e. ./channel-artifacts/Org3.json that contains the Org3 MSP certificates required to join this Org to any channel at any time
	(2) A crt file i.e. ./channel-artifacts/orderer20.crt that contains public certificates of Org3's base orderer required to add this base orderer into system channel to bootstrap
	As a next step copy the ./channel-artifacts/orderer20.crt into channel-artifacts folder of Org2 so that it can bootstrap Org3's base orderer in system channel

In step 8 a genesis file would have been generated in Org2/channel-artifacts/orderer_genesis.pb copy this file to Org3/channel-artifacts/orderer_genesis.pb and then run the following command to start the containers 9. ./fabric-network.sh up

After the containers of Org3 are up, publish it's orderer details by running the command in step 10.