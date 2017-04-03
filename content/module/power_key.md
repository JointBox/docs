---
verbose_name: Power Key
module_name: PowerKey
image: powerkey.jpg
description: "Allows to turn on or off any load. Might be useful for controlling lights."
tags: [ "core", "GPIO", "lights" ]
is_core: true
source_code: /s000pf13/nitro
requires: [ "gpio" ]
---

This is description

## Parameters

* **gpio** GPIO pin identifier. The pin connected to the executive
module (e.g. relay)

## State

State is represented by integer variable which is set to `1` if key
gpio pin has HIGH level and `0` otherwise.

## Actions

* **on** Sets state to `1`
* **off** Sets state to `0`
* **toggle** Switches state to the opposite value
* **state(int val)** Switches state according passed parameter

## Examples

### Controlling lights with a switch

In this example we have 2 devices. A [button](/modules/button)
connected to GPIO pin `PA1` and relay connected to pin `PA6`. Each time
button is pressed relay changes state.

```yaml
  bedroom_lamp:
    module_name: PowerKey
    gpio: PA1

  switch:
    module_name: Button
    gpio: PA6
    pipe:
      click: '#bedroom_lamp.toggle'
```