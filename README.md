
## PROXMOX CONFIGS FOR F5 

* SCSI disk 
* 440fx v8.0
* Memory 8192
* 1 socket 4 cores

## CLI LOGIN

username: root
password: default

## MCPD DAEMON RESTART SOLVE  (V14)

    tmsh stop sys service mcpd
    mkdir /shared/.snapshots_d
    reboot

## CONFIGURE IP FOR MANAGEMENT  (V14)
    tmsh
    modify sys global-settings mgmt-dhcp dhcpv4
    modify sys global-settings mgmt-dhcp enabled
    list /sys management-ip
    quit
    bigstart stop httpd
    bigstart start https


## SSH DAEMON NOT WORKING SOLVE (V14)

    bigstart stop sshd
    ssh-keygen -t rsa -f /config/ssh/ssh_host_rsa_key
    restorecon -rF /config/ssh/ssh_host_*
    bigstart restart sshd 
    journalctl -u sshd

## License Install

Log in to tmsh by entering the following command:
    tmsh

To view the current license details, enter the following command:
    show /sys license

To exit tmsh, enter the following command:
    quit

Using tmsh to install or reactivate the license

Note: Traffic processing is briefly interrupted as the BIG-IP system reloads the new license. This interruption may result in a failover. F5 recommends that you perform the following procedures on the standby BIG-IP device.

Log in to tmsh by entering the following command:
    tmsh

Enter the license key or add-on key, using the following command syntax:
To install or re-activate only the license base registration key, use the following command syntax:

    install /sys license registration-key <License-Key>

To install or re-activate only the add-on key, use the following command syntax:

    install /sys license add-on-keys { <Add-On-Key> }

To install or re-activate the license base registration key and add-on key, use the following command syntax:

    install /sys license registration-key <license-key> add-on-keys { <add-on-key> }

For example:

    install /sys license registration-key ABCDE-ABCDE-ABCDE-ABCDE-ABCDEFG add-on-keys { ABCDEFG-ABCDEFG }

