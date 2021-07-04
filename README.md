# wgconfig-php

Parsing and writing WireGuard configuration files (comment preserving)

WireGuard config files are ini-style. Since all "Peer" sections have the same name, these files cannot be parsed and modified by most modules handling configuration files. Most existing modules are not able to preserve or even add comments when modifying a config file. "wgconfig-php" was created to work with WireGuard configuration files and to preserve comments.

This work was loosely derived from the Python module `wgconfig` https://github.com/towalink/wgconfig by Dirk Henrici.

---

## Features

- Read and parse WireGuard configuration files and make the data available as PHP arrays
- Create new WireGuard configuration files
- Add peers to WireGuard configuration files and delete peers from WireGuard configuration files
- Save and clone WireGuard configuration files
- Comments are preserved when reading and writing WireGuard configuration files
- Leading comments may be added when creating sections or attributes
- Such comments may be deleted when removing sections or attributes

---

## Quickstart

### Reading and parsing an existing WireGuard configuration file

Read and parse the existing WireGuard configuration file `wg0.conf` located in `/usr/local/etc/wireguard`:

```php
require_once('wgconfig.inc');
$wc = new wgconfig('wg0');
$wc.read_file()
print_r($wc->get_interface());
print_r($wc->get_peers());
```

Add a new peer with a comment line before the peer section:
```php
$wc->add_peer('801mgm2JhjTOCxfihEknzFJGYxDvi+8oVYBrWe3hOWM=', '# Newly added peer');
```

Add an attribute to that peer:
```php
$wc->add_peer_attr('801mgm2JhjTOCxfihEknzFJGYxDvi+8oVYBrWe3hOWM=', 'Endpoint', 'wg.example.com:51820', '# Added for demonstration purposes');
```

Write the changes to disk. Comments that were present when reading the file are preserved.
```php
$wc->write_file()
```
