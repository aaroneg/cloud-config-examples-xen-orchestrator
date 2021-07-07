# cloud-config-examples-xen-orchestrator
Since this was hugely frustrating to figure out I'm saving this here.

The following is literally the text of what should go in the network config box in xen orchestra. Obviously you'd need to change the addresses, gateways, search domains etc.

It is critically important that the first line be `#network:`.

```yaml
#network:
    version: 2
    renderer: networkd
    ethernets:
        eth0:
            addresses:
                - 192.168.0.124/24
                - 2001:db8::::1:9f/64
            gateway4: 192.168.0.1
            nameservers:
                search: [example.com]
                addresses: [192.168.0.1, 8.8.8.8]
```

The user config will look similar to this:

```yaml
#cloud-config
hostname: {name}
users:
  - name: jappleseed
    gecos: jappleseed
    primary_group: jappleseed
    groups: adm
    lock_passwd: false
    shell: /bin/bash
    sudo: ALL=(ALL) NOPASSWD:ALL
    ssh_authorized_keys:
      - ssh-rsa KEYCONTENTS user@HOSTNAME

ca-certs:
  trusted: 
  - |
    -----BEGIN CERTIFICATE-----
    # The indented contents of your CA cert go here:
    AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
    AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
    AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
    AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
    -----END CERTIFICATE-----```
