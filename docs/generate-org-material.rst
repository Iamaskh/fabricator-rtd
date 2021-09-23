Generate organization material
=====

Before we go ahead creating either a local or multi-machine network, we have to first create individual scripts for each organization. To do this easily, we have created a script called generate-org which copies the material from /fabric-template folder (see the code above) and parametrizes it according to each organization.

The command to create org material can be run as:

.. code-block:: bash

    	$ ./generate-org.sh {ORG_NAME} {DOMAIN_NAME} {ORG_NUMBER} {ORG_EXPLORER_PORT}

Run this command for each organization (either in the same machine or in separate machines). This command would also download and resolve dependencies if not done already. For more information on dependencies, see the next section.        
 
