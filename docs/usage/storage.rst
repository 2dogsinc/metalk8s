Workload Storage
================

Any workload needs different volumes with different storage capacities
to host its components. These volumes are stored in ``lv``, itself
stored in ``fs``. 

Volumes
-------

Following the total storage capacity needed, establish a number of
volumes and their capacities for each node, as exemplified below:

.. code-block:: yaml

    metalk8s_lvm_lvs_vg_metalk8s:
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
---------

Volumes' capacities can be resized (one or several at once).
Change the volume size value to a higher one and run:

.. code::

  ansible-playbook -i 'your inventory' -t storage playbooks/deploy.yml

Logical volumes are automatically resized.
