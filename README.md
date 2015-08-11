## linuxmuster_net-server-epoptes_via_postsync

[![Travis CI](http://img.shields.io/travis/ypid/ansible-linuxmuster_net-server-epoptes_via_postsync.svg?style=flat)](http://travis-ci.org/ypid/ansible-linuxmuster_net-server-epoptes_via_postsync)
[![Ansible Galaxy](http://img.shields.io/badge/galaxy-ypid.linuxmuster_net–server–epoptes_via_postsync-660198.svg?style=flat)](https://galaxy.ansible.com/list#/roles/4113)
[![Platforms](http://img.shields.io/badge/platforms-debian%20/%20ubuntu-lightgrey.svg?style=flat)](#)
[![GitHub Tags](https://img.shields.io/github/tag/ypid/ansible-linuxmuster_net-server-epoptes_via_postsync.svg)](https://github.com/ypid/ansible-linuxmuster_net-server-epoptes_via_postsync)
[![GitHub Stars](https://img.shields.io/github/stars/ypid/ansible-linuxmuster_net-server-epoptes_via_postsync.svg)](https://github.com/ypid/ansible-linuxmuster_net-server-epoptes_via_postsync)


Configure epoptes on a linuxmuster.net server via postsync.

### Status
Beta.

It has been sucessfully used in postsync and client mode.

### Summary

This role is intended to run against a [linuxmuster.net](https://linuxmuster.net) server and configure [epoptes](http://www.epoptes.org/) for the clients.
It is based on [the documentation at linuxmuster.net](http://www.linuxmuster.net/wiki/anwenderwiki:linuxclient:epoptes).

For configuring the client have a look at the role [`ypid.linuxmuster_net-client-epoptes_via_postsync`](https://galaxy.ansible.com/list#/roles/4114).


### Postsync directory structure

    /var/linbo/linuxmuster-client/image_name
    ├── r23_student
    │   ├── etc
    │   │   ├── default
    │   │   │   └── epoptes-client
    │   │   ├── epoptes
    │   │   │   └── server.crt
    │   │   ├── init.d
    │   │   │   └── epoptes-client
    │   │   └── xdg
    │   │       └── autostart
    │   │           └── epoptes-client.desktop
    │   └── usr
    │       └── local
    │           └── bin
    │               └── epoptes-client-loop.sh
    ├── r23_teacher
    │   ├── etc
    │   │   ├── default
    │   │   │   └── epoptes
    │   │   ├── epoptes
    │   │   ├── init.d
    │   │   │   └── epoptes
    │   │   ├── sudoers.d
    │   │   │   └── ansible-teacher-epoptes-restart
    │   │   └── xdg
    │   │       └── autostart
    │   │           └── epoptes-copy-key.desktop
    │   └── usr
    │       └── local
    │           ├── bin
    │           │   └── epoptes-copy-key.sh
    │           └── share
    │               └── applications
    │                   └── epoptes.desktop

### Installation

This role requires at least Ansible `v1.3`. To install it, run:

```Shell
ansible-galaxy install ypid.linuxmuster_net-server-epoptes_via_postsync
```

To install via git, run either:

```Shell
git clone https://github.com/ypid/ansible-linuxmuster_net-server-epoptes_via_postsync.git ypid.linuxmuster_net-server-epoptes_via_postsync
git submodule add https://github.com/ypid/ansible-linuxmuster_net-server-epoptes_via_postsync.git ypid.linuxmuster_net-server-epoptes_via_postsync
```




### Role variables

List of default variables available in the inventory:

```YAML
---

linuxmuster_net_server_epoptes_room: 'r23'

linuxmuster_net_server_epoptes_room_prefix: ''
linuxmuster_net_server_epoptes_room_suffix: '-*'

linuxmuster_net_server_epoptes_teacher: 'r23pc1.linuxmuster-net.lokal'
## All other systems of that group will be student systems.

linuxmuster_net_server_epoptes_via_postsync_image_name: linux_mint

linuxmuster_net_server_epoptes_via_postsync_wol: g
linuxmuster_net_server_epoptes_port: 789

linuxmuster_net_server_epoptes_socket_group: "teachers"

## Run this role against a client instead against the postsync directory on the server.
# linuxmuster_net_server_epoptes_deploy_on_client: 'student'
#
## Path on the Ansible controller where the public-private-keypair is stored.
# linuxmuster_net_server_epoptes_local_key_path: '/home/user/work/epoptes'

linuxmuster_net_server_epoptes_client_key_dir: '/dev/shm/.k'

linuxmuster_net_server_epoptes_master_name: "Epoptes (iTALC Nachfolger)"
linuxmuster_net_server_epoptes_postsync_script: "/var/linbo/{{ linuxmuster_net_server_epoptes_via_postsync_image_name }}.cloop.postsync"

## Testing postsync template with wanted.yml data structure.
linuxmuster_net_server_epoptes_room_definition:
  - room: '{{ linuxmuster_net_server_epoptes_room }}'
    # room_prefix: "{{ linuxmuster_net_server_epoptes_room_prefix }}"
    # room_suffix: "{{ linuxmuster_net_server_epoptes_room_suffix }}"
    teachers:
    - '{{ linuxmuster_net_server_epoptes_teacher }}'
    - 'r23pc2'
    # students:
    # - 'r23pc4'
    # - 'r23pc5'


## Enforce mode aka sweet revenge mode :) Restart display server if a student tries to kill the epoptes-client.
## WIP
# linuxmuster_net_server_epoptes_enforce: True
linuxmuster_net_display_manager: 'mdm'
```

List of internal variables used by the role:

    linuxmuster_net_server_epoptes_base_client_root_path


### Authors and license

`linuxmuster_net-server-epoptes_via_postsync` role was written by:

- [Robin Schneider](https://github.com/ypid) | [e-mail](mailto:ypid@riseup.net)

License: [AGPLv3](https://tldrlegal.com/license/gnu-affero-general-public-license-v3-%28agpl-3.0%29)

***

README generated by [Ansigenome](https://github.com/nickjj/ansigenome/).
