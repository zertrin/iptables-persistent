iptables-persistent
================================

Based on Debian's iptables-persistent package that load iptables using rules specified at `/etc/iptables/rules`

This one is bit modified to properly handle fail2ban's rules reloading (fail2ban inserts its own rules at the beginning of iptables current ruleset when (re)started) when starting/stopping/reloading iptables's rules via iptables-persistent.

Provided is an example set of rules as quickstart. You should review it and adapt it to your needs.

### Installation

To use:

* copy `iptables-persistent` in `/etc/init.d/` and make it executable 

`cp iptables-persistent /etc/init.d/iptables-persistent
chmod +x /etc/init.d/iptables-persistent`

* copy `iptables-persistent.conf` to `/etc/default/iptables-persistent.conf` and edit it if needed

`cp iptables-persistent.conf /etc/default/iptables-persistent.conf`

* copy `rules` to `/etc/iptables/rules` and edit it to suit your needs

`cp rules /etc/iptables/rules`

* make iptables-persistent to be lauched at startup

`update-rc.d iptables-persistent defaults`
