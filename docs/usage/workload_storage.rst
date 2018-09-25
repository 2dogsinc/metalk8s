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

Configuration layout
--------------------

The configuration can be applied to groups and hosts in two
different ways.

.. note::
   Configuration files are merged for every created host or group.

Groups
******

Create `group_vars/<group name>.yml` or `group_vars/<group name>/<file>.yml`,
where several files can be added.

Hosts
*****

Create `host_vars/<node name>.yml` or `host_vars/<node name>/<file>.yaml`.

.. warning::
   The ansible command above must be run at every addition (deletions are
   not allowed).

Add extra LVs
-------------

It is possible to add extra lvm drive and volume for one node only.

Exemplified below, a default storage configuration:

`group_vars/kube-node/storage.yml`

.. code::

  metalk8s_lvm_vgs = ['vg_metalk8s']
  metalk8s_lvm_drives_vg_metalk8s: ['/dev/vdb']
  metalk8s_lvm_lvs_vg_metalk8s:
    lv01:
        size: 52G
    lv02:
        size: 52G
    lv03:
        size: 52G

In host_vars, create a new file with:

`host_vars/node_1.yml`

.. code::

   metalk8s_lvm_vgs = ['vg_metalk8s', 'mynewvg']
   metalk8s_lvm_drives_mynewvg: ['/dev/vdc']
   metalk8s_lvm_lvs_vg_metalk8s:
     lv01:
        size: 52G
   metalk8s_lvm_lvs_mynewvg:
     lv01:
        size: 1T

Except node_1, every machine has a single `vg_metalk8s` with six LVs
(three specified, three default).
On node_1, there are two VGs (`vg_metalk8s` and `mynewvg`) with four LVs on
`vg_metalk8s` (one specified, three default) and one LV on `mynewvg`.

.. note::
   As the VG name becomes a prefix, several LVs can have the same name.
