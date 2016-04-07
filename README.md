ansible-firewalld-role
=========

Allows you to configure firewalld.

Requirements
------------

Tested on RHEL 7 and CentOS 7 only. 

Ansible 1.9 or above 

Role Variables
--------------

The following variable is used to define the default zone of firewalld:

```
    default_zone: (optional, default: public)
```

For example the default is to set the public zone as default: 

```
    default_zone: public
```

The following variables are used to define the interface of a zone:

```
    firewalld_zone_interface:
      eth0: (optional, default: public for eth0)
```

For example the default is to set eth0 as default for the public zone: 

```
    firewalld_zone_interface:
      eth0: public
```

The following variables are used to define a service rule: 

```
    firewalld_service_rules: 
      service:
        state: (optional, default: enabled)
        zone: (optional, default: public) 
        permanent: (optional, default: true)
        immediate: (optional, default: true)
```

For example the default is to allow SSH in the public zone: 

```
    firewalld_service_rules: 
      ssh:
        state: enabled
        zone: public
        permanent: true
        immediate: true
```

The following variables are used to define a port rule: 

```
    firewalld_port_rules: 
      name:
        port:
        protocol: (optional, default: tcp)
        state: (optional, default: enabled)
        zone: (optional, default: public)
        permanent: (optional, default: true)
        immediate: (optional, default: true)
```

For example the default is to allow SSH on the public zone: 

```
    firewalld_port_rules: 
      ssh:
        port: 22
        protocol: tcp
        state: enabled
        zone: public
        permanent: true
        immediate: true
```

Handlers
--------

These are the handlers that are defined in this role:

    restart firewalld

Example Playbook
----------------

Example with all parameters:
```
    - hosts: server
      become: yes
      become_user: root
      become_method: su
      roles:
        - ansible-firewalld-role
      vars:
        default_zone: public
        firewalld__zone_interface:
          eth0: public
          eth1: internal
        firewalld_service_rules:
          ssh:
            state: enabled
            zone: public
            permanent: true
            immediate: true
        firewalld_port_rules:
          smtp:
            port: 25
            protocol: tcp
            state: enabled
            zone: public
            permanent: true
            immediate: true
```

Example without optional parameters:
```
    - hosts: server
      become: yes
      become_user: root
      become_method: su
      roles:
        - ansible-firewalld-role
      vars:
        firewalld_zone_interface:
          eth1: internal
        firewalld_service_rules:
          ssh:
        firewalld_port_rules:
          smtp:
            port: 25
```

License
-------

MIT

