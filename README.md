CephFS Client
========

Provides an ansible role for configuring cephfs on clients (such as desktops).

Requirements
------------

* You must have a working ceph cluster.
* You must have kernel support for CephFS built into the target's kernel or the packages for FUSE installed.
* You must have client cephx auth ids in the form: client.{{ hostname }}-cephfs
* You must have client keys in the format client.{{ hostname }}-cephfs.keyring in the fetch/{{ cluster }}/etc/ceph/ directory. These will be placed on each client by this role in {{ cephfs_secretpath }} (default: /etc/ceph/) directory and chmod'ed to root-only.
* Only tested on Ubuntu 14.04 and 16.04.1, but probably works on all Debian-like systems, and possibly on all Linux systems with support for Ceph.


Role Variables
--------------

One effectivley mandatory variable:

    cephfs_server: "your.monitor.pool.example.com"

Set that to a DNS address with the montiors you want client to connect to, such as mons.ceph.site.exaample.com or whatever you use.

See the default vars for other options you can use.

Dependencies
------------

No strict dependancies, but you will need your own ceph cluster and probably another role to collect the client keys in your fetch/ directory.

Example Playbook
-------------------------

Examples of using this role:

    - hosts: desktops
      roles:
         - { role: imjustmatthew.cephfs-client, cephfs_server: "mons.ceph.BOS.example.com", cephfs_mountpoint: "/media/ceph",  }

Include some mount options:

    - hosts: backup_servers
      roles:
         - { role: imjustmatthew.cephfs-client, cephfs_server: "mons.ceph.PBI.example.com", cephfs_opts: "noatime,ro",  }


License
-------

GPLv3

