amtc
====

`amtc` - Intel [vPro](http://de.wikipedia.org/wiki/Intel_vPro)/[AMT](http://en.wikipedia.org/wiki/Intel_Active_Management_Technology) mass remote power management tool

features
========

* performs vital AMT operations (info, powerup, powerdown, reset...)
* brutally fast (queries 180 Core i5 PCs in a quarter of a second)
* allows mass-powerups/downs/... using a custom delay
* lightweight C application, only depends on libcurl and pthreads
* currently builds fine on linux and OSX (and windows via cygwin)
* allows quick and comfortable mass-power control via shell (works!) and...
* comes with a web interface for GUI-based
  * power-live-monitoring (works)
  * including OS tcp port probing/detection (works)
  * power/OS-monitoring logging with graphing (undone)
  * remote-management (working on it)
* acts as a tool for flexible and robust scheduled remote power management

The [amtc wiki](https://github.com/schnoddelbotz/amtc/wiki) features more details.

usage
=====

```

 amtc v0.3.0 - Intel AMT(tm) mass management tool 
            https://github.com/schnoddelbotz/amtc

 usage:
  amtc [actions] [options] host [host ...]

 actions:
  -i(nfo) query powerstate via AMT (default)
  -u(p)   powerup given host(s) 
  -d(own) powerdown
  -r      powercycle
  -R      powerreset
  -s(can) [port] - TCP port scan [notyet]
 options:
  -t(imeout) in seconds, for curl and tcp scans [ 5]
  -w(ait)    seconds after each thread created  [ 0]
  -m(aximum) number of parallel workers to use  [40]
  -v(erbosity) increase it by adding more v's
  -j(son) produces JSON output of host states
  -T(LS)  [notyet]
  -S(SH)-scan: probe TCP port 22   for OS detection
  -W(IN)-scan: probe TCP port 3389 for OS detection
  -p(asswdfile) [notyet; export AMT_PASSWORD ]

```

status
======
alpha. just for fun. against all odds. works for me.

building
========
+ OSX: Install XCode including CommandLineTools; type make
+ Debianoid: apt-get install libcurl3 libcurl4-openssl-dev build-essential; type make
+ Windows: install cygwin's curl and pthreads (-dev) packages, make and gcc; type make

todo
====
+ finish port/OS scanner; apply operations only if a given port is open
+ support control commands in amtc-web (info/view only atm)
+ add quiet mode (error-only) (for cron / free scheduled remote power management)
+ add TLS support (for AMT hosts provisioned in enterprise mode)
+ support hosts with AMT < v6.0 ?

alternatives
============
- [amttool](http://www.kraxel.org/cgit/amtterm/tree/amttool):
  Without amttool, there would be no amtc. Thanks! Also supports configuration, which amtc doesn't.
  amttool is implemented in perl and intended for interactive, verbose single-host operation.
  amtc is implemented in C, and by using threads optimized for quick, succinct (non-)interactive mass-operation.
- [amttool_tng](http://sourceforge.net/projects/amttool-tng):
  The next generation. Even more config stuff.
- [vTul](https://github.com/Tulpep/vTul):
  A windows powershell based GUI. Again, completely different story.
- bootstrap your own using the [intel AMT SDK](http://software.intel.com/sites/manageability/AMT_Implementation_and_Reference_Guide)
