Ansible Role: Tentacool
=======================

[![Build Status](https://travis-ci.org/martingalloar/ansible-tentacool.svg?branch=master)](https://travis-ci.org/martingalloar/ansible-tentacool)

An Ansible role that installs [Tentacool](https://github.com/tentacool/tentacool) HPFeeds broker on Debian/Ubuntu.

Requirements
------------

None.


Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

    # The name of the broker
    tentacool_broker_name: '@hp1'
    
    # Port for running the broker
    tentacool_port: 20000
    
    # Max number of concurrent threads
    tentacool_max_thread: 10
    
    # The length of the queue where clients are put before assigning to a thread
    tentacool_queuelen: 64
    
    # Maximum idle time for a thread before is it terminated
    tentacool_idletime: 100

### Authentication

The following variables can be used to build authentication records to use in tentacool:

    # Authentication records
    tentacool_auth: [
      { identifier: "identifier",
        secret: "password",
        publish: "channel.publish",
        subscribe: "channel.subscribe" },
    ]

Dependencies
------------

None.


Example Playbook
----------------

The following example playbook installs Tentacool with the name `honeypot`,
and registers the identity `honeypot` to publish and subscribe to the
`honeypot.events` hpfeed channel:

    - hosts: servers
      roles:
         - { role: martingalloar.tentacool,
             tentacool_broker_name: 'honeypot'
             tentacool_auth: [
               { identifier: "honeypot",
                 secret: "SecretPassword",
                 publish: "honeypot.events",
                 subscribe: "honeypot.events" },
             ]
           }

License
-------

GPL2+


TODO
----

- [ ] Configurable logfile
- [ ] Option to setup MongoDB as authentication store (maybe as a separate role, to avoid adding another dependency)


Author Information
------------------

This role was created by Martin Gallo.
