system_lvm
=========

This role allows you to use the community.general.lvg and community.general.lvol modules to create, resize or remove volume groups and/or logical volumes.

Requirements
------------

ansible >= 2.10

Role Variables
--------------

```
system_lvm:
  first_entry:
    force: ...
    lv:
      - active: ...
        force: ...
        lv: ...
        opts: ...
        pvs: ...
        resizefs: ...
        shrink: ...
        size: ...
        snapshot: ...
        state: ...
        thinpool: ...
    pesize: ...
    pv_options: ...
    pvresize: ...
    pvs: ...
    state: ...
    vg: ...
    vg_options: ...
  second_entry:
    .
    .
    .
  .
  .
  .
```

Dependencies
------------

None

Example Playbook
----------------

#### Create a volume group, create a logical volume:
```
- hosts: servers
  vars:
    system_lvm:
      vol1:
        lv:
          - lv: test1_lv
            size: 512
        pvs: /dev/sdb1
        vg: test1_vg
  roles:
    - turcumihaiioan.system_lvm
```

#### Resize a volume group, resize a logical volume, resize a logical volume and it's filesystem:
```
- hosts: servers
  vars:
    system_lvm:
      vol2:
        lv:
          - lv: test2_lv
            size: 80%PVS
          - lv: test3_lv
            size: 20%PVS
            resizefs: true
        pvresize: true
        pvs: /dev/sdb2
        vg: test2_vg
  roles:
    - turcumihaiioan.system_lvm
```

#### Remove a volume group, remove a volume group with a logical volume, remove a logical volume:
```
- hosts: servers
  vars:
    system_lvm:
      vol3:
        state: absent
        vg: test3_vg
      vol4:
        lv:
          - lv: test5_lv
            state: absent
        state: absent
        vg: test4_vg
      vol5:
        lv:
          - lv: test5_lv
            state: absent
        vg: test4_vg
  roles:
    - turcumihaiioan.system_lvm
```

License
-------

GPL-3.0-only

Author Information
------------------

Role created by Turcu Mihai Ioan
