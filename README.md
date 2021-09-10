![pfFocus](logos/pfFocus.png)

# pfFocus

[![Check](https://github.com/TKCERT/pfFocus/actions/workflows/check.yml/badge.svg)](https://github.com/TKCERT/pfFocus/actions/workflows/check.yml)
[![Docker](https://github.com/TKCERT/pfFocus/actions/workflows/docker.yml/badge.svg)](https://github.com/TKCERT/pfFocus/actions/workflows/docker.yml)

This simple tool allows you to convert a full configuration backup of a *pf*Sense firewall into some meaningful output format, like Markdown or YAML. It enables you to **focus** on the important parts of your firewall configuration and allows you to get a quick overview of the most important settings.

## Requirements

* Python 3.6+
    * defusedxml==0.5.0
    * PyYAML==5.4

## Screenshots

**Before:** Configuration backup as XML

![Configuration backup as XML](screenshots/pfFocus_xml.png)

**After:** Markdown documentation

![System and Interfaces](screenshots/pfFocus_System_Interfaces.png)
![Filter rules](screenshots/pfFocus_Filter_rules.png)

## Features

pfFocus currently supports the following configuration sections:

* Basic system information
* List of interfaces, VLANs, bridges, gateways and static mappings
* List of DHCP ranges and aliases
* NAT rules with alias and interface resolution
* Outbound NAT rules with alias and interface resolution
* Filter rules with alias and interface resolution
* DNS forwarder (DNSmasq) configuration
* OpenVPN server and client configurations
* Syslog and sysctl configuration

## Usage

Main formatting tool: ```pf-format```
```
pf-format
```

Examples:
```
pf-format -i config-backup.xml -f md -o test.md
pf-format -i config-backup.xml -f yaml -o test.yaml
```

Test parsing tool: ```pf-parse```
```
pf-parse [-h] input_path
```

Examples:
```
pf-parse config-backup.xml
```

### Usage via Docker

When using pfFocus via Docker, you don't need to download it from Github, and you don't need to install Python or any libraries. Only Docker is required.

It runs this command inside Docker: `pf-format -q -f md -i - -o -`, which means it works with `STDIN` and `STDOUT` instead of files.

```bash
docker run --rm -i ghcr.io/tkcert/pffocus < input.xml > output.md
```

If you want you can set up an alias for it in bash:

```bash
alias pf-format="docker run --rm -i ghcr.io/tkcert/pffocus"
```

Then you can use it like a normal Unix command, with pipes and redirects:

```bash
pf-format < input.xml > output.md
```

## Roadmap

Some ideas for the future development of pfFocus:

* Producing additional output formats, especially structured formats like CSV.
* Using these structured formats to enable easy diff'ing of configurations.
* Maybe functionality to correlate rule configurations of different firewalls.

## Credits

* Thomas Patzke ([@thomaspatzke](https://github.com/thomaspatzke)) for
    * valuable suggestions and feedback
* Florian Roth ([@Cyb3rOps](https://twitter.com/Cyb3rOps)) for
    * giving it the name *pfFocus*
    * the very nice and gorgeous logo
