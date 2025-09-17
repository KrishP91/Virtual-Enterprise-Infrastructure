# Virtual-Enterprise-Infrastructure
# A six-VM virtual network simulating a startup environment (OpenBSD, FreeBSD, Rocky Linux, Ubuntu, Solaris)
# DNS (BIND), LDAP, PKI, SMTP/IMAP, CUPS print server; automated system configs (NFS, firewalls, Nginx, logging) via Ansible


### OpenBSD (Core Services)
- Role: DNS, LDAP, NTP
- Provides:
  - LDAP authentication to all VMs
  - Domain name resolution
  - NTP time sync

### Ubuntu (Web Server)
- Role: Nginx, Docker-hosted apps
- Uses:
  - NFS from `rocky`
  - LDAP from `openbsd`

### FreeBSD (Mail Server)
- Role: Postfix, Dovecot
- Auth via `openbsd`

...

### Network Topology
- Internal subnet
- NAT to external world (via Proxmox/UTM bridge)
- All hosts resolve DNS via `openbsd`

### Shared Resources
- NFS exported by `rocky`: `/exports/home`, `/exports/logs`
- Central logging to `solaris`: `rsyslog` or `syslog-ng`
