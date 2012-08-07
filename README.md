Linux-HA STONITH module for the Linode API
==========================================

This script implements STONITH using the Linode API -- if a node in your
cluster becomes unavailable, it can be fenced by issuing shutdown/boot/reboot
commands to the API.

Dependencies
------------

python-pycurl (not absolutely necessary, but python-linode uses it for better
SSL certificate validation):

    - apt-get install python-pycurl

The Python bindings to the Linode API:

    - sudo pip install python-linode

Configuration
-------------

Copy this script to /usr/lib/stonith/plugins/external, and make it
executable.

**IMPORTANT!** Make sure your Linodes have labels that match their node names in
your HA configuration. This is crucial for obtaining their Linode IDs for the
API calls.

Example CRM configuration snippet:

    primitive st-linode stonith:external/linode \
            params hostlist="node1 node2 node3" api_key="YOUR_API_KEY"
    clone fencing st-linode


Copyright (c) 2012 Fairview Computing, LLC.
