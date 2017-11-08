[![Travis CI](https://img.shields.io/travis/inofix/ansible-acme-tiny-request.svg?style=flat)](http://travis-ci.org/inofix/ansible-acme-tiny-request)


Acme-Tiny Setup
===============

This is an ansible role for creating a certificate request, and just the request. For signing certificates, take a look at inofix.acme-tiny-sign.

This role is meant to be run on any host that needs certificates for itself.
 If the host is not accessible via web - or does not use the inofix.acme-tiny-sign role for other reasons - a solution must be provided to transfer the cert-request forth and the final certificate back from this host to the acme-host. See inofix.acme-tiny-cron-proxy for an example.

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

 # ansible-galaxy install inofix.acme-tiny-request

Requirements
------------

* Ansible >2.0
* Python2/3 on target host
* Generic UNIX with FHS
* Sudo
* Systemd (per default)

Role Variables
--------------

* app\_\_acme\_\_tiny\_\_config\_dir - optional, default='/etc/ssl/acme-tiny'
* app\_\_acme\_\_tiny\_\_openssl\_config - optional, default='/etc/ssl/openssl.cnf'
* app\_\_acme\_\_tiny\_\_domain - optional, default='example.com'
* app\_\_acme\_\_tiny\_\_cert\_name - optional, auto
* app\_\_acme\_\_tiny\_\_cert\_path - optional, default='/etc/ssl/acme-tiny/{{ app\_\_acme\_\_tiny\_\_cert\_name }}'
* app\_\_acme\_\_tiny\_\_cert\_dir - optional, auto
* app\_\_acme\_\_tiny\_\_key - optional, auto
* app\_\_acme\_\_tiny\_\_request - optional, auto
* app\_\_acme\_\_tiny\_\_key\_length - optional, default=4096

Dependencies
------------

* inofix.acme-tiny-setup

Example Playbook
----------------

    - hosts: servers
      roles:
         - inofix.acme-tiny-setup

License
-------

GPLv3

Author Information
------------------

* Michael Lustenberger at [inofix.ch](http://www.inofix.ch)
