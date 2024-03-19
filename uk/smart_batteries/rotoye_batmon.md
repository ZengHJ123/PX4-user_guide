# Rotoye Batmon

[Rotoye Batmon](https://rotoye.com/batmon/) is a kit for adding smart battery functionality to off-the-shelf Lithium-Ion and LiPo batteries. It can be purchased as a standalone unit or as part of a factory-assembled smart-battery.

:::note
At time of writing you can only use Batmon by [building a custom branch of PX4](#build-px4-firmware). Support in the codeline is pending [PR approval](https://github.com/PX4/PX4-Autopilot/pull/16723).
:::


![Rotoye Batmon Board](../../assets/hardware/smart_batteries/rotoye_batmon/smart-battery-rotoye.jpg)

![Pre-assembled Rotoye smart battery](../../assets/hardware/smart_batteries/rotoye_batmon/smart-battery-rotoye-pack.jpg)


## Де купити

[Rotoye Store](https://rotoye.com/batmon/): Batmon kits, custom smart-batteries, and accessories


## Wiring/Connections

The Rotoye Batmon system uses an XT-90 battery connector with I2C pins, and an opti-isolator board to transmit data.

![Board connections](../../assets/hardware/smart_batteries/rotoye_batmon/smart-battery-rotoye-connection.png)

Більш детальну інформацію можна знайти [тут](https://github.com/rotoye/batmon_reader)


## Налаштування програмного забезпечення

### Створення прошивки PX4

1. Clone or download [Rotoye's fork of PX4:](https://github.com/rotoye/PX4-Autopilot/tree/batmon_4.03)
   ```sh
   git clone https://github.com/rotoye/PX4-Autopilot.git
   cd PX4-Autopilot
   ```
1. Checkout the *batmon_4.03* branch
   ```sh
   git fetch origin batmon_4.03
   git checkout batmon_4.03
   ```
1. [Build and upload the firmware](../dev_setup/building_px4.md) for your target board

### Налаштування параметрів

У *QGroundControl*:
1. Set the following [parameters](../advanced_config/parameters.md):
   - `BATx_SOURCE` to `External`,
   - `SENS_EN_BAT` to `true`,
   - `BAT_SMBUS_MODEL` to `3:Rotoye`
1. Open the [MAVLink Console](https://docs.qgroundcontrol.com/master/en/analyze_view/mavlink_console.html)
1. Start the [batt_smbus driver](../modules/modules_driver.md) in the console. For example, to run two BatMons on the same bus:
   ```sh 
   batt_smbus start -X -b 1 -a 11 # External bus 1, address 0x0b  
   batt_smbus start -X -b 1 -a 12 # External bus 1, address 0x0c
   ```

## Детальна інформація

[Quick Start Guide](https://rotoye.com/batmon-tutorial/) (Rotoye)