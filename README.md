This is the Arduino code for the implementation of a XAAR XJ128 inkjet printhead to generate aerosol droplets by Xavier Lefebvre. 

Last update : August 2024

# XAAR XJ128

## Background

The Xaar 128 is a piezoelectric inkjet printhead used in large format vinyl sign-making. Most inkjet printheads are “bubble jet”: They work by superheating a fraction of the ink in a chamber, turning it into gas, which expands to force the remainder of the ink out of a nozzle. Superheating limits the range of materials that can be used in these printheads. Piezoelectric printheads are less common, and since they use a mechanical operation to force fluid out of a nozzle, they don’t have to modify the state of the fluid to operate, and can work with a broader range of materials.

## Parts List
- Xaar XJ128 Blue
- Sunfounder 2 Channel 5V Relay Board
- 2 x 36V DC power supplies
- Arduino Uno
- Breadboard, hookup wire, etc.

## Driving the Xaar 128
- 1mhz CLK to drive signal logic in printhead ICs.
- Data is loaded via SPI interface.
- SCK for the SPI interface is independent of CLK above.
- 2 shift registers, each hold 64 bits of data corresponding to 128 nozzles.
- State machine for one print cycle:
  - READY (output from Xaar 128) is HIGH (okay to load data)
  - Enable nSS2, Clock in 64 bits.
  - Disable nSS2.
  - Enable nSS1, Clock in 64 bits.
  - Disable nSS1.
  - nFIRE (active LOW) input to Xaar 128 indicates that data is loaded and ready to fire.
  - READY goes LOW when firing nozzles.
  - READY returns to HIGH

## Xaar 128 Operations Guide
Not available from the Xaar website (please add more sources):
- [Unofficial Source](http://d1.amobbs.com/bbs_upload782111/files_36/ourdev_619324HXZTX0.pdf)
## References

- http://ytec3d.com/forum/viewtopic.php?t=47
- https://www.youtube.com/watch?v=dnBx0aCWNms
