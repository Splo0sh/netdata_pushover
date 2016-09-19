# README #

## Table of Contents ##
<!-- MarkdownTOC depth=0 -->

- [Introduction](#introduction)
- [Requirements](#requirements)
- [Installation](#installation)
- [Known Bugs/Issues](#known-bugsissues)
- [Version History](#version-history)
- [Contact](#contact)

<!-- /MarkdownTOC -->

## Introduction ##

This is a shell script for using the [Pushover](https://pushover.net/) push service with [netdata](https://github.com/firehol/netdata/) alarms.


## Requirements ##

* Pushover application on Computer or Smartphone
* App token from Pushover website
* User token from Pushover client


## Installation ##

**UPDATE:** Was integrated into netdata [alarm-notify.sh](https://github.com/firehol/netdata/pull/919).

Copy the `alarm-pushover.sh` shell script to the netdata's plugin folder, which by default is `/usr/libexec/netdata/plugins.d/`.
The config file `health_pushover_tokens.conf` goes to netdata's config directory, which by default is "/etc/netdata/".

Once the Pushover client is installed on your phone or computer, you need to create an account to receive a user token. This is needed so the push reaches your device. Generate an app token at https://pushover.net and insert that and the usertoken into the `healt_pushover_tokens.conf` file.

Further help for pushover: [https://pushover.net/faq](https://pushover.net/faq)


To activate the push notification for an alarm, open its config file and add/change the `exec` line to `exec: /usr/libexec/netdata/plugins.d/alarm-pushover.sh`.

e.g.: `nano /etc/netdata/health.d/net.conf`
```
# check if an interface is dropping packets
# the alarm is checked every 10 seconds
# and examines the last 30 minutes of data

template: 30min_packet_drops
      on: net.drops
  lookup: sum -30m unaligned absolute
   every: 1m
    crit: $this > 0
   units: packets
    info: dropped packets in the last 30 minutes
    exec: /usr/libexec/netdata/plugins.d/alarm-pushover.sh
```


## Known Bugs/Issues ##

Bugs:
* No known bugs at the moment

Issues:
* No known issues


## Version History ##

v0.1:
* initial release


## Contact ##

Who do I talk to?

* Repo owner or admin
* Other community or team contact

