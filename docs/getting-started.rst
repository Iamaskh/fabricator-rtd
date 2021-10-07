##################
Getting Started
##################

*****************
Prerequisites
*****************
* docker (`install <https://docs.docker.com/engine/install>`__)
* docker-compose (`install <https://docs.docker.com/compose/install>`__)
* curl (`install <https://help.ubidots.com/en/articles/2165289-learn-how-to-install-run-curl-on-windows-macosx-linux>`__)
* yq (`install <https://github.com/mikefarah/yq#install>`__)

*****************
Download Fabric dependencies
*****************

Fabric Dependencies can be downloaded to start a new fabric network v2.0.1 from scratch using this command:

.. code-block:: bash

    $ ./fabric-dependencies.sh -s -- <fabric_version> <fabric-ca_version> <thirdparty_version>
    $ ./fabric-dependencies.sh -s -- 2.0.1 1.4.6 0.4.18 



