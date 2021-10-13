##################
Adding organizations
##################

This is a basic tutorial on setting up 3 organizations, use the following commands: 


Organization 1
##############

To read all the help regarding commands use: :code:`./fabric-network.sh help.`

Generate the crypto material for *organization 1* and start it. 

.. code-block:: bash
    
    $ ./fabric-network.sh generate-crypto
	
    $ ./fabric-network.sh up

Organization 2
##############
Bootstrap *organization 2* from *organization 1*, Copy the shared orderer certificates (:file:`OrdererSharedCerts` folder) from first organization's :file:`channel-artifact` folder in *organization 2* i.e. :file:`Org2/OrdererSharedCerts`. Once the shared certificates are placed as required run following commands.


.. code-block:: bash

       $ /fabric-network.sh generate-crypto

The above command generates 2 important files for bootstrapping
(1) A json file i.e. :file:`./channel-artifacts/Org2.json` that contains the Org2 MSP certificates required to join this Org to any channel at any time
(2) A crt file i.e. :file:`./channel-artifacts/orderer10.crt` that contains public certificates of Org2's base orderer required to add this base orderer into system channel to bootstrap
As a next step copy the :file:`./channel-artifacts/orderer10.crt` into channel-artifacts folder of Org1 so that it can bootstrap Org2's base orderer in system channel


.. code-block:: bash

       $ ./fabric-network.sh add-remote-orderer 10


In above command 10 refers to *orderer number*. Since we are bootstrapping *Organization 2's base orderer* it is 10, it should be 20 for *organization 3* and so on..
As a result of this command for *base orderer 10* a genesis file will be generated in :file:`channel-artifacts` folder i.e. :file:`./channel-artifacts/orderer_genesis.pb` of *organization 1*
This generates a genesis file would have been generated in :file:`./channel-artifacts/orderer_genesis.pb` copy this file to :file:`./Org2/channel-artifacts/orderer_genesis.pb`. 

**Next step: Copy the** :file:`channel-artifacts/orderer_genesis.pb` **of organization 1 into** :file:`channel-artifacts/orderer_genesis.pb` **of the organization 2.**

Then run the following command to start the containers:

.. code-block:: bash

       $ ./fabric-network.sh up


After the containers of *organization 2* are up, publish it's orderer details by running the following command:

.. code-block:: bash

	$ ./fabric-network.sh publish-remote-orderer 10


The above command ensures that the base orderer of *organization 2* is published and now peers can contact this as an active orderer in the network. 
This command must be run after the containers of *organization 2* are up and running.

Organization 3
##############

To start bootstraping Org3, Copy the shared orderer certificates (:file:`OrdererSharedCerts` folder) from first/2nd organization's :file:`channel-artifact` folder in Org3 i.e. :file:`Org3/OrdererSharedCerts`. Once the shared certificates are placed as required run following commands.

.. code-block:: bash

	$ ./fabric-network.sh generate-crypto 

This command generates 2 important files for bootstrapping
(1) A json file i.e. :file:`./channel-artifacts/Org3.json` that contains the Org3 MSP certificates required to join this Org to any channel at any time
(2) A crt file i.e. :file:`./channel-artifacts/orderer20.crt` that contains public certificates of Org3's base orderer required to add this base orderer into system channel to bootstrap
As a next step copy the :file:`./channel-artifacts/orderer20.crt` into channel-artifacts folder of Org2 so that it can bootstrap Org3's base orderer in system channel

To Bootstrap Org3 from Org2:

.. code-block:: bash

	$ ./fabric-network.sh add-remote-orderer 20

In above command 20 refers to orderer number. Since we are bootstrapping Org3's base orderer it is 20, it should be 30 for Org4 and so on..
As a result of this command for base orderer20, a genesis file will be generated in :file:`channel-artifacts` folder i.e. :file:`channel-artifacts/orderer_genesis.pb`

**Next step: Copy the** :file:`channel-artifacts/orderer_genesis.pb` **into** :file:`channel-artifacts/orderer_genesis.pb` **of the Org3** 

In the above step, a genesis file would have been generated in :file:`Org2/channel-artifacts/orderer_genesis.pb` copy this file to :file:`Org3/channel-artifacts/orderer_genesis.pb` and then run the following command to start the containers 

.. code-block:: bash

	$ ./fabric-network.sh up

After the containers of Org3 are up, publish it's orderer details by running the command in the following step:

.. code-block:: bash

	$ ./fabric-network.sh publish-remote-orderer 20

The above command ensures that the base orderer of Org3 is published and now peers can contact this as an active orderer in the network. 
This command must be run after the containers of Org3 are up and running.	


.. note::

    You can follow the steps given above in this tutorial in the similar way to set up upto *N organizations*.