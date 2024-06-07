# ESPHome gateway for Aldes T.One® AIR / AquaAIR

**WARNING: for now this is all 100% theoritical and 0% tested. Be sure to know what you're doing!***

## Hardware

+ D1 mini
+ RS485/TTL converter ([AliExpress](https://fr.aliexpress.com/item/1005006340391490.html))
+ 12V to 5V buck converter ([AliExpress](https://fr.aliexpress.com/item/1005006486270630.html))

### Wiring the controller

+ D1 mini TX pin (GPIO01) => RS485/TTL converter RXD pin
+ D1 mini RX pin (GPIO03) => RS485/TTL converter TXD pin
+ D1 mini 3V3 pin => => RS485/TTL converter VCC pin
+ D1 mini G pin (ground) => RS485/TTL converter GND pin (the pin on the same side as TX, RX & VCC)
+ D1 mini G pin (ground) => buck converter OUT- pin
+ D1 mini 5V pin => buck converter OUT+ pin

### Wiring T.One Modbus with the controller

**Be sure to know exactly what you're doing. You can void your garanty, damage your Aldes device or even worse. Turn off the T.One's power at circuit breaker before you open it and begin wiring the Modbus.**

+ T.One ModBus A pin => RS485/TTL A+ pin
+ T.One ModBus B pin => RS485/TTL B- pin
+ T.One Modbus ground pin (1st one on the left) => buck converter IN- pin
+ T.One Modbus ground pin (1st one on the left) => RS485/TTL converter ground pin (the pin on the same side as A+ & B-)
+ T.One Modbus +12V pin => buck converter IN+ pin

## Software

### Short-term goal

This first and most simple implementation uses ESPHome [Modbus components](https://esphome.io/components/modbus).

See [esphome-aldes-tone.yaml](esphome-aldes-tone.yaml)

### Mid-term goal

We will need better, because with the implementation above, we won't have Climate entities in Home Assistant, but only sensors, selects, number inputs etc.

Indeed, currently there is no Modbus platform for Climate in ESPHome, so no native ESPHome Climate component can be passed to Home Assistant.

But good news: we could be able to use [hass-template-climate](https://github.com/jcwillox/hass-template-climate) to create Climate entities with HA templates, by assembling the Modbus components we just created in the 1st milestone.

### Long-term goal

Ultimately, we would want to have an ESPHome native climate component. This is possible by developing and using an ESPHome [external component](https://esphome.io/components/external_components.html), or by adding the Modbus platform in ESPHome Climate component (that last one seems a definitively harder solution unless ESPHome devs step in).