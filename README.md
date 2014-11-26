udev_rename_netiface
====================

This role creates `udev` rules to rename network interfaces. The goal is to reuse
the information from the configuration of the `network_interface` role.


Examples
--------

Example of how to define udev rewrite rules:

```
---

# This is a playlist example
- hosts: myhost
  vars:
    # First we define the data structure with the interface(s). It is the same
    # data scructure used by the 'network_interface' role with the difference
    # that only the 'device' and the 'hwaddr' params are required.
    network_ether_interfaces:
     - device: eth0
       hwaddr: 12:34:56:78:90:ab

  roles:
    # Here we load the our role which creates the udev rule(s) based on the
    # information from the 'network_ether_interfaces' data structure
    - role: udev_rename_netiface
```

Example of how to clear the `udev` rules file:

```
---

# This is a playlist example
- hosts: myhost
  vars:
    # This variable specifies whether to clear the udev rules or not. It can be
    # used when udev rename rules are anymore required.
    udev_rename_netiface_clear: true

  roles:
    # Here we load the our role which creates the udev rule(s) based on the
    # information from the 'network_ether_interfaces' data structure
    - role: udev_rename_netiface
```


Role variables
--------------

The main variable is the `network_ether_interfaces` which defines the network
interfaces like like in the `network_interface` role. If the `network_interface`
role is used, only the 'hwaddr' should be addedd to each network interface which
is required to be renamed.

There is also a boolean variable `udev_rename_netiface_clear` specifying whether
to clear the udev rules or not. It can be used when udev rename rules are not
anymore required.

Last variable is `udev_rename_netiface_enabled` which allows to disable the
`udev` rules file creation completely.


Dependencies
------------

* [`network_interface`](https://galaxy.ansible.com/list#/roles/3) role (optional)


License
-------

MIT


Author
------

Jiri Tyr <jiri.tyr@gmail.com>
