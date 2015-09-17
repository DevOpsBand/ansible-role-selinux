Ansible Selinux Role
=======

An Ansible role to manage SELinux mode/policy.


Role Variables
--------------

    # SELinux mode (enforcing / permissive / disabled)
    selinux_state: disabled

    # SELinux policy (targeted / mls)
    selinux_policy: targeted

    # Reboot server if SELinux configuration has been changed
    selinux_reboot: false

    # Message for shutdown
    selinux_reboot_message: SELinux configuration updates triggered

    # Delay before polling the host
    selinux_reboot_wait_delay: 10

    # Pause after reboot
    selinux_reboot_pause_: 10


Example Playbook
----------------

Disable SELinux and reboot server:

    - hosts: all
      roles:
        - { role: selinux, selinux_reboot: true }

Configure SELinux in enforcing mode (you have to reboot server manualy after):

    - hosts: all
      roles:
        - { role: selinux, selinux_state: enforcing }


Role Testing
------------

    vagrant up --no-provision
    vagrant provision


Author Information
------------------

Borys Borysenko / borys.borysenko@gmail.com
