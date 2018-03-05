[![Travis CI](https://img.shields.io/travis/inofix/ansible-acme-request.svg?style=flat)](http://travis-ci.org/inofix/ansible-acme-request)


Acme Setup
==========

This is an ansible role for creating a certificate request, and just the request. For signing certificates, take a look at inofix.acme-tiny-sign.

This role is meant to be run on any host that needs certificates for itself
or signs any for some other host.

If the host uses certificates, a private key and a CSR are created.
For hosts that only do the signing for other hosts, the CSRs are deployed.
(See inofix.acme-setup for an overview.)

The development of this role was started within zwischenloesung.acme-tiny-setup which was later split.

Why we do not use one of the existing roles?

* For the first reason read the section "Promise" below. We need something reliable.
* This role will be used by [maestro](https://github.com/inofix/maestro) and must follow the logic used there. (Of course, the role can be used without maestro..)


State
-----

preSTABLE (Feature-Freeze/RC)


Promise
-------

Sure, this role may change in the future, but we will only expand features to not break backwards compatibility.

If radical changes should become necessary, a new role will be created, probably with a version suffix...


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

* app\_\_acme\_\_os\_\_cert\_group - optional, default='{{ default\_\_acme\_\_group }}'
* app\_\_acme\_\_user - optional, default='acme'
* app\_\_acme\_\_group - optional, default='acme'
* app\_\_acme\_\_home - optional, default='/var/lib/acme'
* app\_\_acme\_\_config\_dir - optional, default='/etc/ssl/acme'
* app\_\_acme\_\_openssl\_config - optional, default='/etc/ssl/openssl.cnf'
* app\_\_acme\_\_domain - optional, default=[ {domain='example.com'} ]
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

(See inofix.acme-setup)

License
-------

GPLv3

Author Information
------------------

* Michael Lustenberger at [inofix.ch](http://www.inofix.ch)
