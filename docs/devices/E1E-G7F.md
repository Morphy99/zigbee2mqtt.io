---
title: "Sengled E1E-G7F control via MQTT"
description: "Integrate your Sengled E1E-G7F via Zigbee2MQTT with whatever smart home
 infrastructure you are using without the vendors bridge or gateway."
---

*To contribute to this page, edit the following
[file](https://github.com/Koenkk/zigbee2mqtt.io/blob/master/docs/devices/E1E-G7F.md)*

# Sengled E1E-G7F

| Model | E1E-G7F  |
| Vendor  | Sengled  |
| Description | Smart switch  |
| Exposes | action, linkquality |
| Picture | ![Sengled E1E-G7F](../images/devices/E1E-G7F.jpg) |

## Notes


### Pairing
Factory reset the switch by pressing and holding the on and off buttons at the same time for at least 33 seconds. The indicator will start flashing, indicating a successul reset. The device will enter pairing mode for one minute. If the device is not connected in one minute, you must restart the pairing process.


### Long press action
The device will sometimes output a single push in addition to a long press. You can mitigate this by using the Debounce device configuration. Refer to *[How to use device type specific configuration](../information/configuration.md)*.



## Exposes
### Action (enum)
Triggered action (e.g. a button click).
Value can be found in the published state on the `action` property.
It's not possible to read (`/get`) or write (`/set`) this value.
The possible values are: `on`, `up`, `down`, `off`, `on_double`, `on_long`, `off_double`, `off_long`.

### Linkquality (numeric)
Link quality (signal strength).
Value can be found in the published state on the `linkquality` property.
It's not possible to read (`/get`) or write (`/set`) this value.
The minimimal value is `0` and the maximum value is `255`.
The unit of this value is `lqi`.

## Manual Home Assistant configuration
Although Home Assistant integration through [MQTT discovery](../integration/home_assistant) is preferred,
manual integration is possible with the following configuration:


{% raw %}
```yaml
sensor:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    value_template: "{{ value_json.action }}"
    icon: "mdi:gesture-double-tap"

sensor:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    unit_of_measurement: "lqi"
    value_template: "{{ value_json.linkquality }}"
    icon: "mdi:signal"
```
{% endraw %}


