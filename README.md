
kvm_host       [![Build Status](https://travis-ci.org/lorephoenix/ansible-kvm_host.svg?branch=master)](https://travis-ci.org/lorephoenix/ansible-kvm_host)
=========

The kvm_host role will install KVM packages on a host. It is also able to manage storage pools.

        git clone https://github.com/lorephoenix/ansible-kvm_host kvm_host


Requirements
------------

A RHEL derivative GNU/Linux system on a x86 hardware that supports virtualization extensions (Intel VT or AMD-V).

Role Variables
--------------

#### Default variables for the role

1. defaults/main.yml


        profile_default:
            libvirt_default_uri: 'qemu:///system' 
            libvirt_pools: 
                - '{{ libvirt_pool_default }}' 

        libvirt_pool_default:
            name: default
            path: /var/cached/libvirt

- profile_**name**: &emsp;a profile with an unique and specific name which require some variables<br />
    
  - libvirt_default_uri: <br />
  &emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;libvirt supports many different kind of virtualization (often referred to as "drivers" or "hypervisors").<br />
  &emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;Specify which driver a connection refers to.<br />
  &emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;qemu:///system connects to a system mode daemon<br />

  - libvirt_pools: <br />
  &emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;a list of storage pool(s)<br />

- libvirt_pool_**name**: &nbsp;a storage pool with an unique and specific name<br />
  - name: &emsp;&emsp;&nbsp;storage pool name<br />
  - path: &emsp;&emsp;&nbsp;&nbsp;&nbsp;the path of the storage<br />


#### Other variables for the role

1. vars/RedHat_7.yml

The variable file will be used when the OS host is part of the OS family RedHat running version 7.

        os_supported:               <boolean data type>
        libvirt_service_name:       <service unit>
        libvirt_owner:              <local libvirt user>
        libvirt_group:              <local libvirt group>
        libvirt_selinux_setype:     <SELinux Type for the object>

        # List of packages to install by default on any rhel family system.
        libvirt_base_pkgs:          <distro packages to install KVM/qemu>


Dependencies
------------

<ul><li>Ansible >= 2.4</li></ul>

Example Playbook
----------------

This is an example playbook:

    - hosts: localhost
      remote_user: ansible
      become: true
      become_method: sudo
      become_user: root
      roles:
      - role: kvm_host 
        libvirt_profile: "{{ profile_default }}"

License
-------

MIT

Author Information
------------------

- Christophe Vermeren | [GitHub](https://github.com/lorephoenix) | [Facebook](https://www.facebook.com/cvermeren)

