
##PROXMOX CONFIGS FOR F5 
SCSI disk 
440fx v8.0
Memory 8192
1 socket 4 cores



##MCPD DAEMON RESTART SOLVE 
tmsh stop sys service mcpd
mkdir /shared/.snapshots_d
reboot

tmsh
 modify sys global-settings mgmt-dhcp dhcpv4
 modify sys global-settings mgmt-dhcp enabled
 list /sys management-ip
 quit
 
bigstart stop httpd
bigstart start https


##SSH DAEMON NOT WORKING SOLVE
bigstart stop sshd
ssh-keygen -t rsa -f /config/ssh/ssh_host_rsa_key
restorecon -rF /config/ssh/ssh_host_*
 
bigstart restart sshd
 
journalctl -u sshd


