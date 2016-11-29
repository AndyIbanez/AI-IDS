# AI-IDS
A small, configurable, PHP and iptables-based IDS for Unix servers.

## 1. Introduction

AI IDS is a small IDS I created to keep track of break-in attempts into my servers. It was designed with the following goals:

1. It must be very easy to install and configure.
2. It must be very easy to extend. Currently I only care about about SSH and SMTP break-in attempts, but you can extend it protect other services as long as they produce logs that contain an IP address. (info on this soon).
3. It must be flexible. You can currently edit most aspects of the IDS through the `config.ini` file, including but not limited to whitelisted IP's, whitelisted countries, etc..

Like many other similar tools, this tool scans the system logs for break-in attempts. In Ubuntu Servers, it will scan `/var/log/auth.log` for SSH attacks and `/var/log/mail.log` for SMTP attacks. You can extend it to scan any other logs. If your distro is not supported out of the box, you can configure the logs that it will scan for the included services (SSH and SMTP) (see config.ini).

This tool uses [FreeGEOIP](https://freegeoip.net/) to get the countries for all the IPs that get banned. This service allows up to 10000 calls per hour, which is more than enough for small to medium servers. To use the IDS on bigger servers with more frequent attacks, you might need to host the service yourself and configure the IDS to use your self-hosted version (see config.ini).

## 2. Installation
## 3. Upgrading
## 4. config.ini

|-------------|--------------|--------------|-----------|-------------|
| **Config Value** | **Default Value(s)** | **Since** | **Notes**| **Required** |
|----|----|-----|-----|------|
## 5. Examples
### 5.1 `POST_BAN_SCRIPTS` examples.

## 6. Future plans

I'd like this IDS to provide the following features in the future.

1. Logging. I'd like it to use the standard Unix logging to write into syslog or into its custom log. Ideally it would write banning information (including the IP, blocked ranges, and country), every time it starts running, and when it has unbanned an IP (including the same info as banning info).
2. I'd like to provide a few command line tools to see statistics about the IDS. For example, I'd like to have a command, `aiids show top` that would list the top countries with the most number of bans. `aiids show banned` to list the currently banned IPs. `aiids history ip` to see the banning history of a given IP, and so on. The database lays the groundwork to implement this functionality. The sky is the limit!