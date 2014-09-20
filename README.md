iptables-persistent
===================

This is a **fork** of Debian's *iptables-persistent* package that loads iptables rules using rules specified at `/etc/iptables/rules`

**UPDATE 2014-09-20**: The *iptables-persistent* package in Debian **jessie** has significanlty changed compared to the previous version, and has somehow been renamed to *netfilter-persistent*. This script is not related to *netfilter-persistent* at all.

This version is modified to **properly handle fail2ban's rules reloading** when starting/stopping/reloading iptables's rules via iptables-persistent (fail2ban inserts its own rules at the _beginning_ of iptables current ruleset when (re)started). If fail2ban is not installed, iptables-persistent will ignore any action related to file2ban.

For **IPv6** enabled servers, ip6tables rules management is properly handled too, by activating the corresponding parameter in the configuration file (see below).

An example set of rules is included as quickstart. It is pretty restrictive: forwarding is disabled and only DNS, ping and SSH are allowed inbound by default. **You MUST review it and edit it to suit your needs!**.

### Installation

To use:

* copy the init.d script `iptables-persistent` to `/etc/init.d/` and make it executable 

* copy `iptables-persistent.conf` to `/etc/default/iptables-persistent.conf` and **edit it to suit your needs**

* copy `rules` to `/etc/iptables/rules` and **edit it to suit your needs**

* copy `ipv6_rules` to `/etc/iptables/ipv6_rules` and **edit it to suit your needs** (you can copy this file even if you don't activate IPv6 support in the configuration, it will be ignored)

* make iptables-persistent to be lauched at startup

`update-rc.d iptables-persistent defaults`

### Configuration variables

Edit `/etc/default/iptables-persistent.conf` to set the following parameters:

* **SAVE_NEW_RULES** (default: 0) - if set different than 0 then the current iptables ruleset will be saved with iptables-save when iptables-persistent is stopped (or restarted)

* **MODULES** (default: "") - a space-separated list of the modules that iptables-persistent should load/unload. Useful to activate FTP connection tracking for example.

* **IPV6** (default: 0) - if set different than 0 it will additionnaly use ip6tables to handle the loading/unloading of the ruleset stored at `/etc/iptables/ipv6_rules`

* **ENABLE_ROUTING** (default: 0) – if set different than 0 then routing is enabled (in `/proc/sys/net/ipv4/ip_forward` and `/proc/sys/net/ipv6/conf/all/forwarding`), otherwise it’s not.
