# USB-C connector
I have a "cheap" USB-C connector (very similart to [this one](https://www.cuidevices.com/product/resource/ujc-hp-3-smt-tr.pdf)) that has only 6 pins. It is power only and should be solderable by hand.

No footprints in kicad for this cheap USB-C model that has only 6 pins. I found these footprints on [GitHub](https://github.com/jenschr/USB-C-Connectors/tree/master/Kicad/Footprints). One of them (TYPE-C-31-M-17) seem to match the connector I have.


## USB-C LiPo charger from SparkFun
 - [Datasheet](https://www.distrelec.ch/Web/Downloads/_t/ds/PRT-15217_eng_tds.pdf)
 - The two VBUS pins are shorted together. So are grounds.

## Design

### USB-C Power
Useful info from this [StackOverflow thread](https://electronics.stackexchange.com/a/327946):
- CC pins should both be pulled down by a 5.1k resistor.

#### Connector
### LIR2450
- 120-ish mAh capacity
- 45mA charging current

### Battery charger IC
- [MCP73831](https://www.sparkfun.com/datasheets/Prototyping/Batteries/MCP73831T.pdf)
- The charging current is programmable via the R_prog resistor:
    I_reg = 1000 V / R_prog
    => For a 45mA ccurrent:
    R_prog = 1000 / 45e-3 = 22.2k 

Nice! This value (22k) is the exact same one as used in [this charger](https://www.theledart.com/collections/usb-powered/products/lir2450-battery-charger). I could probably use 2 * 47k in parallel, since I have these already (although I might need to get 5.1k anyway...).
