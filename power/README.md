# power

A (very) configurable and (hilariously) over-engineered power (AC and battery) status blocklet for [i3blocks](https://vivien.github.io/i3blocks/).

| Appearance | Description |
| ---	     | ---         |
|![](screenshots/on_ac_summary.png)             | AC connected |
|![](screenshots/on_bat_summary.png)            | AC disconnected, battery discharging |
|![](screenshots/on_ac_charging_summary.png)    | AC disconnected, battery charging |
|![](screenshots/on_ac_no_summary.png)          | AC connected, no summary |
|![](screenshots/on_bat_no_summary.png)         | AC disconnected, battery discharging, no summary |
|![](screenshots/on_ac_charging_no_summary.png) | AC disconnected, battery charging, no summary |


# Dependencies

* python3
* Linux kernel 2.6.0+ (for `sysfs`)

# Installation

* Copy the script into your directory of choice, e.g. ~/.i3blocks/blocklets
* Give it execution permission (`chmod +x power`)
* Add the script to your i3blocks config, for example:

```ini
[power]
command=$SCRIPT_DIR/power
markup=pango
interval=1
```

# Configuration

Configuration parameters can be passed by:
* command line arguments (e.g. `$ power -S -p 15 -A`)
* "instance" in the blocklet's section of the `i3blocks` config file, e.g.:
	```ini
	[power]
	...
	instance=-S -p 15 -A
	...
	```
* shell environment variables (e.g. `$ bat_show_summary=no bat_crit_percent=15 ac_show=no power)`
* if using a recent enough i3blocks version (see [here](https://github.com/vivien/i3blocks/issues/374#issuecomment-489406732)), by dynamic block properties in `i3blocks` config file, e.g.:
	```ini
	[power]
	...
	bat_show_summary=no
	bat_crit_percent=15
	ac_show=no
	...
	```
**NOTE:** `Shell ENV` overrides `dynamic prop` overrides `instance` overrides `CLI`


| Default? | Option                                                    | CLI / instance   | Shell ENV / dynamic prop   |
| :---:    | ---                                                       | ---              | ---                        |
|          | Print help/usage and exit                                 | `-h`             | N/A                        |
|          | Enable debug messages to STDERR                           | `-d`             | `debug=$TRUE`              |
|          | Print config to STDERR                                    | `-c`             | `show_config=$TRUE`        |
| Y        | Show summarized stats if multiple batteries present       | `-s`             | `bat_show_summary=$TRUE`   |
|          | Show stats for each battery if multiple batteries present | `-S`             | `bat_show_summary=$FALSE`  |
| 10%      | Set battery critical level                                | `-p $NUMBER`     | `bat_crit_percent=$NUMBER` |
| Y        | Use battery last full capacity                            | `-f`             | `bat_full_type=last`       |
|          | Use battery design (factory) capacity                     | `-F`             | `bat_full_type=design`     |
| Y        | Show battery [dis]charging duration                       | `-t`             | `bat_show_time=$TRUE`      |
|          | Don't show battery [dis]charging duration                 | `-T`             | `bat_show_time=$FALSE`     |
| Y        | Show AC state                                             | `-a`             | `ac_show=$TRUE`            |
|          | Don't show AC state                                       | `-A`             | `ac_show=$FALSE`           |

* **`$TRUE`** means one of `y`, `yes`, `true`
* **`$FALSE`** means one of `n`, `no`, `false`
* **`$BOOL`** means one of `$TRUE`, `$FALSE`
* **`$NUMBER`** means int or float (e.g. 9, 17.0, 56.75)

