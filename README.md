# OPNSense Ping Check

This is a simple utility script that checks if a monitored interface has an
IP address and if ping commands succeed. If either fails, it resets the
monitored interface.

## Warning

Use with care. This script resets the interface when it doesn't have an IP or can't ping.
Ultimately, this script could interrupt connectivity if configured improperly.

## Installation

 - Copy ```ping-check``` to ```/usr/local/etc/rc.d/ping-check```.

 - Edit the script for your interface/desired ping IPs, settings, etc.

 - Set the permissions on the file to 755 (```chmod 755 /usr/local/etc/rc.d/ping-check```).

 - Copy ```actions-pingcheck.conf``` to ```/usr/local/opnsense/service/conf/actions.d/actions-pingcheck.conf```

 - Restart ConfigD (```service configd restart```).

 - Add a new Cron task in the OPNSense UI under System -> Settings -> Cron.
   Use */5 for the minutes and * for everything else. (This will run the check every 5 minutes.)
   Use ping_check for the command and then apply.

  - Monitor the logs via ```tail -f /var/log/system/latest.log``` for pingcheck output.

## Credit

This is largely based on [marjohn56's forum post](https://forum.opnsense.org/index.php?topic=18865.msg86224#msg86224) and [angryoso's reddit post](https://www.reddit.com/r/OPNsenseFirewall/comments/x1yke6/is_there_a_ping_watchdog_to_restart_the_device_if/) with some of my own touches/tweaks.
