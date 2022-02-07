Role Name
=========

This role installs Unbound, a validating, recursive, caching DNS resolver. In
its current state the role allows for a pre-defined list of sources
(whitelisting) to use the configured instance of Unbound as recursing
nameserver. It validates DNSSEC and allows you to configure your own set of
upstream resolvers.

The following features are included and can be configured through variables:

* [DoT](https://datatracker.ietf.org/doc/html/rfc7858) (DNS over TLS), you need to supply your own certificates
* [DoH](https://datatracker.ietf.org/doc/html/rfc8484) (DNS Queries over HTTPS), you need to supply your own certificates

The following features are currently missing / not yet implemented:

* chroot
* Ability to change working directory
* Ability to have more than one forward zones
* Ability to configure the trust-anchor manually
* Ability to serve local zones
* [RPZ](https://dnsrpz.info/) (Response Policy Zones)
* [dnstap](https://dnstap.info/)
* [DNSCrypt](https://www.dnscrypt.org/)

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
log_queries: "yes"
log_replies: "yes"
identity: Query me baby one more time!
upstream_resolvers:
  # All default servers are hosted by non-profits
  # who claim to not log
  - 5.1.66.255 # Freifunk Munich
  - 37.235.1.174 # freedns.zone
  - 172.104.49.100 # freedns.zone
remote_control: "yes"
control_interface: 127.0.0.1
dot: no
dot_key: # The full local path to your key for DoT
dot_crt: # The full local path to your certificate for DoT
doh: no
doh_key: # The full local path to your key for DoH
doh_crt: # The full local path to your certificate for DoH

```

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: gmmi.unboundsible }

License
-------

WTFPL

Author Information
------------------

For any problems with this role, please open an issue on [Github](https://github.com/gmmi/Unboundsible/issues).
