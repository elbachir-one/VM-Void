# Setup Virt Manager For Void Linux.

### Installation.

`$ sudo xbps-install -S virt-manager libvirt qemu openbsd-netcat dnsmasq vde2 bridge-utils`

### Setup.

`$ sudo usermod -aG kvm <username>`

`$ modprobe kvm-<your CPU>`

`$ sudo usermod -a -G libvirt <username>`

### Configuration.

`$ sudo vim /etc/libvirt/libvirtd.conf`

- Uncomment this lines.
> listen_tls = 0
> unix_sock_group = "libvirt"
> unix_sock_ro_perms = "0777"
> unix_sock_rw_perms = "0770"
> unix_sock_dir = "/run/libvirt"
> auto_unix_ro = "polkit" >>> auto_unix_ro = "none"
> auto_unix_rw = "polkit" >>> auto-unix_rw = "none"

Save and exit.

`$ sudo vim /etc/libvirt/libvirt.conf`

- Uncomment.
> uri_default = "qemu:///system"

Save and exit.

`$ sudo vim /etc/libvirt/qemu.conf`

Go to line 519.

- Uncomment line 519 and 523.
> user = "<username>"
> group = "libvirt"

### Enable Services.

1. `$ sudo ln -s /etc/sv/libvirt /var/service/`

2. `$ sudo ln -s /etc/sv/virtlogd /var/service/`

3. `$ sudo reboot`

### End.
- Download an ISO.
- Create a virtual machine.
