Role Name
=========

This role installs Unbound, a validating, recursive, caching DNS resolver. The
following features are currently missing / not yet implemented:

* chroot
* Ability to change working directory
* Ability to have more than one forward zones
* [RPZ](https://dnsrpz.info/) (Response Policy Zones)
* [dnstap](https://dnstap.info/)
* [DNSCrypt](https://www.dnscrypt.org/)
* [DoH](https://datatracker.ietf.org/doc/html/rfc8484) (DNS Queries over HTTPS)
* DNSSEC

The following features are currently missing and will not be implemented:

* cachedb
* Views
* DNS64
* Rate-limiting
* Stub Zones
* Authority Zones

Requirements
------------

None.

Role Variables
--------------

```
interfaces:
  - 0.0.0.0                                                                                                                                   
  - ::0                                                        
port: 53
do_ipv4: yes                                                           
do_ipv6: yes                                                        
acl:                                         
  - range: 127.0.0.0/8                               
    state: allow                
  - range: 0.0.0.0/0                                    
    state: drop                                                                
  - range: ::1                        
    state: allow                                         
  - range: ::0/0                                                         
    state: drop                
username: unbound
```

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

WTFPL

Author Information
------------------

For any problems with this role, please open an issue on [Github](https://github.com/gmmi/Unboundsible/issues).
