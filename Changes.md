
### 1.06  2019-12-19

- don't try using Net::IP when it's not installed, fixes #8
- format Changes to markdown

### 1.05  2016-12-28

- make new sshd error 'maximum authentication attempts exceeded for root' a naughy condition.
- improve the --update function

### 1.04  2016-06-11

- invalid users are naughty

### 1.03  2015-07-14

- change shebang: /usr/bin/env perl -> `which perl`

### 1.02  2015-07-02

- changed shebang: /usr/bin/perl -> /usr/bin/env perl

### 1.01  2015-06-20

- try loading Net::IP early, set $has_netip
- move "or die..." clause to prevent an innocuous perl 5.20 warning
- if LWP::UserAgent not installed, try using curl, wget, or fetch

### 1.00  2015-05-30

- pass perl critic
- count root attempts as naughty (was failed)
- updated version check to GitHub URL

### 0.28  2013-12-10

- added fix for FTP log parsing, m/ / -> m/\s+/ for WS split
- added vpopmail vchkpw-smtp parsing (limit SMTP brute-force)
- added check_sentry NRPE plugin, for Nagios monitoring

### 0.27  2013-12-03

- added fix for ssh log parsing, m/ / -> m/\s+/ for WS split
- added dovecot log parsing (limit POP & IMAP brute-force)

### 0.26

- added the skeleton of a CPAN dist
- fix for unblacklist not removing from tcpwrappers (sn3ak)

### 0.25  2013-04-02 -mps

- Adds IPv6 support if Net::IP is installed
- switched from file/dir to DB|GDBM|NDBM (whichever is installed)
- automatically imports old format into DB (uses FAR less disk space)
- reporting even a million connections is practically instant
- added error messages where failures were previously handled silently

### 0.22  2012-03-07 -mps

- adjusted SYNOPSIS docs so usage syntax is clearer -ian
- added POD docs for update feature

### 0.21  2010-01-03 -mps

- removed wc TODO after testing. Using wc is no faster than perls builtin methods. Added notes to EFFICIENT portion of man page.

### 0.20  2010-06-03 -mps

- POD cleanups

### 0.19  2010-04-22 -mps

- added methods _unblock_tcpwrappers, _unblock_pf, unblock_ipfw. When unblocking an IP, also remove the IP from the tcpd/firewall

### 0.18  2010-04-22 -mps

- added FTP log parsing
- properly account for FreeBSD + sshd + PAM logins
- if an IP is whitelisted and blacklisted, remove from blacklist
- IPs were getting whitelisted and blacklisted, because the do_???list subs were not returning a success code "do_ and exit;". Added missing result code and altered methods to not depend on them "do_; exit;".
- sentry.pl wasn't being installed unless --update was selected. If no version is installed, install anyway.
- when doing an IP report, show the log file entries if --verbose
- if FTP logs are enabled but not found, report error.

### 0.17  2010-01-18 -mps

- updates to pod docs and comments. -mps
- added a couple more sshd log pattern matches
- reworked the --update feature, works better.

### 0.16  2009-06-15 -mps

- ssh log entries that didn't meet the listed criteria were not being counted, preventing the 10 strikes and you're out rule from kicking in

### 0.15  2009-06-09 -mps

- added ssh probe detection in log parser (spurred on by Kevin Golding)

### 0.14  2009-04-15 -mps

- rewrote portions of the pod docs
- added method version_check, (checks tnpi web site for latest version)
- abstracted self_update and configure_tcpwrappers out of check_setup

### 0.12  2009-04-14 -mps

- pf table in docs was sentry, updated to sentry_blacklist (make docs match the code (thanks Kevin Golding).
- pfctl add/remove was not working properly. Fixed and tested.

### 0.11  2009-03-01 -mps

- fixed some bugs in the POD documentation
- skip setup checks when --help is selected

### 2009-03-01 -mps

- added --help option, based on usability study
- sprinkled a few comments in various places
- added a few more file tests before attempting to open file handles
- added better error handling for file accessing methods
- added placeholder _parse_mail_logs

### 2009-02-28 -mps

- CentOS 5.2 logs this IP to syslog: 24.19.45.95 but the 'address' it logs to hosts via %a is ::ffff:208.75.177.98. Sure would be nice if that change was documented in hosts_access(5).
- warn if unable to determine syslog location for sshd

### 2009-02-27 -mps

- discovered and worked around an 'interesting' problem in external files referenced by some implementations of tcpwrappers
- fixed a copy/paste induced bug preventing delist from working on whitelist
- updated syslog finding script to be more robust on various platforms
- added checks for read permission to $root_dir before attempting to report or setup

### 2009-02-26 -mps

- firewalls off by default
- if selected, report is dispatched first
- script will self-install itself in $root_dir if it doesn't exist there
- don't require an IP for reports
- added warnings when common and important operations fail
- added report summary (-v -r)
- added pod documentation

### 2009-02-25 -mps

- reworked the tcpwrappers black/whitelisting after discovery that libwrap doesn't include the very handy file include feature that tcpwrappers has on FreeBSD and Linux
- if hosts.allow and deny are missing, auto-configure them
- added default log locations for numerous platforms
