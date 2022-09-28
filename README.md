# Setup Virt Manager For Void Linux.

### Installation.

`$ sudo xbps-install -S virt-manager libvirt qemu openbsd-netcat dnsmasq vde2 bridge-utils`

### Setup.

`$ sudo usermod -aG kvm <username>`

`$ modprobe kvm-<your CPU>`
For AMD use kvm-amd & for Intel use kvm-intel .

`$ sudo usermod -a -G libvirt <username>`

### Configuration.

`$ sudo vim /etc/libvirt/libvirtd.conf`

- Uncomment this lines.
1. listen_tls = 0
2. unix_sock_group = "libvirt"
3. unix_sock_ro_perms = "0777"
4. unix_sock_rw_perms = "0770"
5. unix_sock_dir = "/run/libvirt"
6. auto_unix_ro = "polkit" >>> auto_unix_ro = "none"
7. auto_unix_rw = "polkit" >>> auto-unix_rw = "none"

Save and exit.

`$ sudo vim /etc/libvirt/libvirt.conf`

- Uncomment.
1. uri_default = "qemu:///system"

Save and exit.

`$ sudo vim /etc/libvirt/qemu.conf`

Go to line 519.

- Uncomment line 519 and 523.
1. user = "your username"
2. group = "libvirt"

### Enable Services.

1. `$ sudo ln -s /etc/sv/libvirtd /var/service/`

2. `$ sudo ln -s /etc/sv/virtlogd /var/service/`

3. `$ sudo reboot`

### End.
- Download an ISO.
- Create a virtual machine.


### Note.
If you have DHCPCD for network, you need to change it up to NetworkManager. Just to be able to connect via ssh to the virtual machine.

1. `$ sudo xbps-install -S NetworkManager`
2. `$ sudo sv down dhcpcd`
3. `$ sudo rm /var/service/dhcpcd`
4. `$ sudo ln -s /etc/sv/NetworkManager /var/service/`
5. `$ sudo ln -s /etc/sv/dbus /var/service/`
6. `$ sudo reboot`
