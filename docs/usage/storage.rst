Storage
=======

.. todo::
   Intro sentence.

Volumes
-------

Any workload needs different volumes with different storage capacities
to store its components. Following the total storage capacity needed,
establish a number of volumes and their capacities for each node, as
exemplified below:

.. code-block:: yaml

    metalk8s_lvm_lvs_vg_metalk8s: ['/dev/vdb']
        lv01:
            size: 52G
        lv02:
            size: 52G
        lv03:
            size: 52G
        lv04:
            size: 11G
        lv05:
            size: 11G
        lv06:
            size: 11G
        lv07:
            size: 5G
        lv08:
            size: 5G

Resize lv
------------

.. todo::
   Document resizing.
