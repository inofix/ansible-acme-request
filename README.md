[![Travis CI](https://img.shields.io/travis/inofix/ansible-acme-request.svg?style=flat)](http://travis-ci.org/inofix/ansible-acme-request)



Acme Setup
==========

This is an ansible role for creating a certificate request, and just the request. For signing certificates, take a look at inofix.acme-tiny-sign.

This role is meant to be run on any host that needs certificates for itself.
 If the host is not accessible via web - or does not use the inofix.acme-tiny-sign role for other reasons - a solution must be provided to transfer the cert-request forth and the final certificate back from this host to the acme-host. See inofix.acme-cron-proxy for an example.

The development of this role was started within zwischenloesung.acme-tiny-setup which was later split.

Why we do not use one of the existing roles?

* For the first reason read the section "Promise" below. We need something reliable.
* This role will be used by [maestro](https://github.com/inofix/maestro) and must follow the logic used there. (Of course, the role can be used without maestro..)


State
-----

UNSTABLE! We are just migrating from zwischenloesung.acme-tiny-setup.


Promise
-------

Sure, this role may change in the future, but we will only expand features to not break backwards compatibility.

If radical changes should become necessary, a new role will be created, probably with an 'ng' or version suffix...


Installation
------------

 # ansible-galaxy install inofix.acme-request

Requirements
------------

* Ansible >2.0
* Python2/3 on target host
* Generic UNIX with FHS
* Sudo
* Systemd (per default)

Role Variables
--------------

* app\_\_acme\_\_config\_dir - optional, default='/etc/ssl/acme'
* app\_\_acme\_\_openssl\_config - optional, default='/etc/ssl/openssl.cnf'
* app\_\_acme\_\_domain - optional, default='example.com'
  * actually here you can provide a app\_\_acme\_\_domain\_request if the list is not the same as for the app\_\_acme\_\_domain (e.g. if a host signs both certificates for itself and as a proxy for remote service hosts)
* app\_\_acme\_\_cert\_name - optional, auto
* app\_\_acme\_\_cert\_path - optional, default='/etc/ssl/acme/{{ app\_\_acme\_\_cert\_name }}'
* app\_\_acme\_\_cert\_dir - optional, auto
* app\_\_acme\_\_key - optional, auto
* app\_\_acme\_\_request - optional, auto
* app\_\_acme\_\_key\_length - optional, default=4096
* fqdn - optional, default={{ ansible\_fqdn | d(inventory\_hostname ) }}
* workdir - optional, default='/tmp', used to store requests for remote signing

Dependencies
------------

* inofix.acme-setup

Example Playbook
----------------

    - hosts: servers
      roles:
         - inofix.acme-request

License
-------

GPLv3

Author Information
------------------

* Michael Lustenberger at [inofix.ch](http://www.inofix.ch)
