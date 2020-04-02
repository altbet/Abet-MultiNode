# Nodemaster

The **Nodemaster** scripts is a collection of utilities to manage, setup and update masternode instances.

I am quite confident this is the single best and almost effortless way to setup different crypto masternodes, without bothering too much about the setup part.

If this script helped you in any way, please contribute some feedback. BTC donations also welcome and never forget:

**Have fun, this is crypto after all!**

```
BTC  19U8Jgyb38XnbGyQq3SHXS614pmLbvwKeZ
```


Feel free to use my reflink to signup and receive a bonus w/ vultr:
<a href="https://www.vultr.com/?ref=7424168"><img src="https://www.vultr.com/media/banner_2.png" width="468" height="60"></a>

If you wish to use DigitalOcean you can use this referal link but the following guide will only go over Vultr.
Deploy your next app in seconds. Get $100 in cloud credits from DigitalOcean using my link: <a href="https://m.do.co/t/a3f23a15f9af">"<img src="https://blog.microdreamit.com/wp-content/uploads/2019/08/Digital-Ocean-Credit.gif" width="468" height="60"></a>

**NOTE on the VPS choice for starters**

**Vultr** is highly recommended for this kind of setup. I created an [easy step-by-step guide for the VPS provider vultr](/docs/masternode_vps.md) that will guide you through the hardest parts.

---

## About / Background

A very in depth guide for beginners (https://steemit.com/masternodes/@swcrypto/ccbc-easy-guide-to-setup-multiple-masternodes-on-1-vps) 

Many masternode crypto currencies only have incomplete or even non-existing instructions available how to setup a masternode from source.

This project started as handy bash script to setup my $PIVX masternodes in 2016 when there was almost zero documentation and anything that existed was either $DASH specific, sucked and in most cases both. For that reason, i started to work on a not-so-sucking way to install a lot of different masternodes with next to none manual intervention.

If you are not already aware, visit the project site and join the slack. The website at [https://pivx.org/](https://pivx.org/) is also well worth a visit.

Many people use binaries, end of with an insecure configuration or fail completely. This is obviously bad for the stability of the individual network.

After doing hundreds of masternode installations in the past two years, i decided to share some of my existing auto-install and management scripts with the community to work on a generalised & reliable setup for all masternode coins.

Comparing with building from source manually, you will benefit from using this script in the following way(s):

* 100% auto-compilation and 99% of configuration on the masternode side of things. It is currently only tested on a vultr VPS but should work almost anywhere where IPv6 addresses are available
* Developed with recent Ubuntu versions in mind, currently only 16.04 is supported
* Installs 1-100 (or more!) masternodes in parallel on one machine, with individual config and data
* Compilation is currently from source for the desired git repo tag (configurable via config files)
  Some security hardening is done, including firewalling and a separate user
* Automatic startup for all masternode daemons
* This script needs to run as root, the masternodes will and should not!
* It's ipv6 enabled, tor/onion will follow

## Installation

SSH to your VPS and clone the Github repository:

```bash
git clone https://github.com/altbet/Abet-MultiNode.git && cd Abet-MultiNode
```

Install & configure your desired master node with options:

```bash
./install.sh -p abet
```

## Examples for typical script invocation

These are only a couple of examples for typical setups. Check my [easy step-by-step guide for [vultr](/docs/masternode_vps.md) that will guide you through the hardest parts.

**Install & configure 4 ABET masternodes:**

```bash
./install.sh -p abet -c 4
```

**Update daemon of previously installed ABET masternodes:**

```bash
./install.sh -p abet -u -n "6"
```

**Install 6 ABET masternodes with the git release tag "tags/v3.4.0.0"**

```bash
./install.sh -p abet -c 6 -r "tags/v3.4.0.0"
```

**Wipe all ABET masternode data:**

```bash
./install.sh -p abet -w
```

**Install 2 ABET masternodes and configure sentinel monitoring:**

```bash
./install.sh -p abet -c 2 -s
```

## Options

The _install.sh_ script support the following parameters:

| Long Option  | Short Option | Values              | description                                                         |
| :----------- | :----------- | ------------------- | ------------------------------------------------------------------- |
| --project    | -p           | project, e.g. "abet"| shortname for the project                                           |
| --net        | -n           | "4" / "6"           | ip type for masternode. (ipv)6 is default                           |
| --release    | -r           | e.g. "tags/v3.4.0.0"| a specific git tag/branch, defaults to latest tested                |
| --count      | -c           | number              | amount of masternodes to be configured                              |
| --update     | -u           | --                  | update specified masternode daemon, combine with -p flag            |
| --sentinel   | -s           | --                  | install and configure sentinel for node monitoring                  |
| --wipe       | -w           | --                  | uninstall & wipe all related master node data, combine with -p flag |
| --help       | -h           | --                  | print help info                                                     |
| --startnodes | -x           | --                  | starts masternode(s) after installation                             |

## Troubleshooting the masternode on the VPS

If you want to check the status of your masternode, the best way is currently running the cli e.g. for $MUE via

```
/usr/local/bin/abet-cli -conf=/etc/masternodes/abet_n1.conf getinfo

{
"version": 3040100,
  "protocolversion": 71000,
  "services": "NETWORK/BLOOM/",
  "walletversion": 61000,
  "balance": 0.0,
  "zerocoinbalance": 0.00000000,
  "blocks": 74831,
  "timeoffset": -313,
  "connections": 16,
  "proxy": "",
  "difficulty": 3057.202499631633,
  "testnet": false,
  "moneysupply": 2177318.59247520,
  "keypoololdest": 1576542282,
  "keypoolsize": 1001,
  "unlocked_until": 0,
  "paytxfee": 0.00000000,
  "relayfee": 0.00010000,
  "staking status": "Staking Active",
  "errors": ""
}
```
# Helpful Commands

## Start Coin on initial install
```
/usr/local/bin/activate_masternodes_abet
```
## Stop coin
```
/usr/local/bin/abet-cli -conf=/etc/masternodes/abet_n1.conf stop
```
## Start Coin
```
/usr/local/bin/abetd -conf=/etc/masternodes/abet_n1.conf
```
## Getinfo
```
/usr/local/bin/abet-cli -conf=/etc/masternodes/abet_n1.conf getinfo
```


# Help, Issues and Questions

I activated the "[issues](https://github.com/masternodes/vps/issues)" option on github to give you a way to document defects and feature wishes. Feel free top [open issues](https://github.com/masternodes/vps/issues) for problems / features you are missing here: [https://github.com/masternodes/vps/issues](https://github.com/masternodes/vps/issues).

I might not be able to reply immediately, but i do usually within a couple of days at worst. I will also happily take any pull requests that make masternode installations easier for everyone ;-)

If this script helped you in any way, please contribute some feedback. BTC donations also welcome and never forget:

**Have fun, this is crypto after all!**

```
BTC  19U8Jgyb38XnbGyQq3SHXS614pmLbvwKeZ
```

## Management script (not yet implemented)

The management script release will follow within the next couple of days.

| command                               | description                                  |
| :------------------------------------ | -------------------------------------------- |
| nodemaster start abet (all\|number)   | start all or a specific pivx masternode(s)   |
| nodemaster restart abet (all\|number) | stop all or a specific pivx masternode(s)    |
| nodemaster stop abet (all\|number)    | restart all or a specific pivx masternode(s) |
| nodemaster cleanup abet (all\|number) | delete chain data for all pivx masternodes   |
| nodemaster status abet (all\|number)  | systemd process status for a pivx masternode |
| nodemaster tail abet (all\|number)    | tail debug logs for a pivx masternode        |

# Todo

* provide my Dockerfile & Vagrantfile
* write more test cases
* implement a binary option (?)
* output all supported cryptos as list within help

# Errors

* currently not fully idempotent

Ping me at contact@marsmenschen.com for questions and send some crypto my way if you are happy.

**Have fun, this is crypto after all!**

```
BTC  19U8Jgyb38XnbGyQq3SHXS614pmLbvwKeZ
```
