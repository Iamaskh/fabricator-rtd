##################
Adding Peers
##################

The following commands can run from any organization as required:

To add a new peer

.. code-block:: bash

	$ ./fabric-network.sh add-peer

To join the newer peer to existing channel


.. code-block:: bash
    
        If need be, you can join this newer peer to the existing using the join-channel-peer command by changing the peer <number> as required
	
	$ ./fabric-network.sh join-channel-peer 2 channelall