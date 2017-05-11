---
verbose_name: Power Key
module_name: PowerKey
image: powerkey.jpg
description: "Allows to turn on or off any external load. Might be useful for controlling lights."
tags: [ "core", "GPIO", "lights", "featured" ]
is_core: true
source_code: https://github.com/JointBox/jointbox/blob/master/src/modules/power_key/__init__.py
requires: [ "gpio" ]
---

The main purpose of the module is controlling external load via GPIO.
Any type of the device which uses discrete digital interface should be
supported. The most common scenario is relay board based on electro
magnetic relays. There are multiple variations of these boards available
on the market including multi-chanel modules, modules based on solid state relays.

Also it might be useful to control simple transistor if it is compatible
with GPIO voltage of your board.

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

In this example we have 2 devices. A [button](/module/button)
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