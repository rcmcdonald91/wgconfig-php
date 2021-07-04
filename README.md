# wgconfig-php

## Usage
```php
require_once('wgconfig.inc');

$wc = new wgconfig('wg0');

print_r($wc->get_interface());

print_r($wc->get_peers());

$wc->set_interface_attr('MTU', 1420);

$wc->write_file();

print_r($wc->get_conf_string());
```
