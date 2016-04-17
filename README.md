# kvm / 1und1.de

1und1.de does not allow brigding the external interface (eth0)
This Files may help to configure BaseSystem with firewall and clients.

VM01: IPFIRE
- Internal RED-Interface on "...'default':NAT" via DHCP
- Internal GREEN-Interface on "Bridge privatebr0...vmnet1" with 192.168.201.1

VM0X: ????
- Internal Network on "Bridge privatebr0...vmnet1" via DHCP
- PORTFORWARDING, Intrusion-Detection from IPFIRE

....

System: Ubuntu 14.04.X with KVM
- aptitude install bridge-utils qemu-kvm libvirt-bin haveged

Filespostitions: 
- /etc/libvirt/qemu/networks/default.xml
- /etc/network/interfaces
- /etc/libvirt/hooks/qemu

