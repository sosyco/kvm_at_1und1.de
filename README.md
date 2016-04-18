# kvm / 1und1.de / RootServer-Systeme
keine Haftung für Fehler/Schäden durch die Nutzung dieser Dateien.

1und1.de erlaubt aus Sicherheitsgründen nicht die Verbindung einer VM via Bridge auf EHT0 mit dem Internet.
Die hier abgelegten Dateien können helfen die Anbindung via NAT für das 
folgende Szenario einfach zu ermöglichen:

VM01 
Name: IPFIRE 
Quelle: http://www.ipfire.org/download
Funktion: Der Firewall sichert die Netzwerkverbindung zweischen dem externe Netz (Virtuelle Netzwerk'default':NAT) und dem internen Netz (Bridge privatebr0:Wirtgerät vnet1)
Konfiguration:
RED: Virtuelle Netzwerk'default':NAT; DHCP; (192.168.122.2)
GREEN: Bridge privatebr0:Wirtgerät vnet1; 192.168.201.1; DHCP-Server

VM02...VMXX
System: Beliebig
Konfiguration:
ETH0: Bridge privatebr0:Wirtgerät vnet1; DHCP
Portzuweisung von IPFIRE aus.

------------------------------------------------------------
BasisSystem: Ubuntu 14.04.X with KVM
# aptitude install bridge-utils qemu-kvm libvirt-bin haveged

Dateien und Funktion: 
/etc/libvirt/qemu/networks/default.xml
- Änderung der Defaultnetzwerkeinstellungen.
- Nur noch 192.168.122.2 wird zugewiesen
- Nur noch IPFIRE RED-Schnittstelle mit dem Netz 'default' verbinden

/etc/network/interfaces
- Anlegen der Schnittstelle privatebr0 ohne direkte Verbindung nach Aussen.
- Netzwerkschnittstelle für alle anderen VMs

/etc/libvirt/hooks/qemu
- Script um alle definierten Portranges via NAT von ETH0 auf 192.168.122.2 umzuleiten.
