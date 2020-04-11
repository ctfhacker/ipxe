# iPXE for Bochs

iPXE is one way of leveraging a PXE enabled kernel in Bochs. This repo should help quickly make an image 
to use in Bochs. The second time I forgot how to make one of these, I decided to just create this repo to
never have to worry again.

## Modification 

Modify the `boot.ipxe` script with the filename you want iPXE to reach out for.

```
#!ipxe
ifopen net0

set net0/ip 192.168.10.2
set net0/netmask 255.255.255.0
set net0/dns 192.168.10.1
set net0/gateway ${net0/dns}
set net0/next-server ${net0/dns}
set net0/filename <REPLACEME>.boot

# Verify settings with user
# config net0

chain ${net0/filename}
```

## Install

On linux:

```
sudo apt install liblzma5 liblzma-dev isolinux genisoimage
git clone git://git.ipxe.org/ipxe.git
cd ipxe/src
make
make bin/ipxe.iso EMBED=../../boot.ipxe
```

## Bochsrc

Add the following line to the bochsrc

```
ata0-master: type=cdrom, path="/path/to/ipxe.iso", status=inserted
```
