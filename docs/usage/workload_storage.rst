Workload Storage
================

Any workload needs different volumes with different storage capacities
to host its components. These volumes are stored in :term:`LVM LV`.

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

Resize LVs
----------

Volumes' capacities can be resized (one or several at once).
Change the volume size value to a higher one and run:

.. code::

  ansible-playbook -i <inventory>/hosts -t storage playbooks/deploy.yml

Logical volumes are automatically resized.

Add extra LVs
-------------

It is possible to add extra lvm drive and volume for one node only.

1. Add a new vg and list its volume sizes, specifying the drives.

.. code::

  metalk8s_lvm_vgs = ['vg_metalk8s', 'mynewvg']
  metalk8s_lvm_drives_vg_metalk8s: ['/dev/vdb']
  metalk8s_lvm_drives_mynewvg: ['/dev/vdc']
  metalk8s_lvm_lvs_vg_metalk8s:
     <Volumes list>
  metalk8s_lvm_lvs_mynewvg:
     lv01:
        size: 1T

2. Create a host_vars dir similar to group_vars dir, and put the node name
where to add the extra volume: :file:`<node_name>.yaml`

.. note::
   Volumes for vg_metalk8s do not need to be specified again, as they are
   listed in the ``group_vars`` dir already.
