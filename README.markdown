Nagios Plugins
=============

mc-package-check
-------------
MCollective wrapping Nagios check that reports any hosts with a package
installed that shouldn't be or lacking a package that should be
installed.

$ mc-package-check bluetooth fail-when-present

mc-service-check
-------------
MCollective wrapping Nagios check that reports any hosts running a
service that should be stopped or hosts not running a service that
should be started.

$ mc-service-check bluetooth fail-when-stopped
