# yamaha-rx-v363-ir-codes
IR Hex codes I have uncovered for a Yamaha RX-V363 reciever while working on an ESPHome-based IR Remote.

Relevant ESPHome code below creates a Home Assistant service that can be called to send verious hex codes directly from the Home Assistant frontend, without specifying switches in the ESPHome yaml.

Majority of codes are also confirmed to work with the RX-V863 receiver. Please refer to the PDF with more codes, eg. for the Yamaha RX-V863 the "off" command only turns off main, by combining the "off" command with 0x7EBB zone 2 will also turn off.

```*.yaml
api:
  password: !secret api_pw
  reboot_timeout: 0s
  services:
    - service: remote_2code
      variables:
        rc_code_1: int
        rc_code_2: int
      then:
      - remote_transmitter.transmit_pioneer:
          rc_code_1: !lambda 'return rc_code_1;'
          rc_code_2: !lambda 'return rc_code_2;'
          repeat:
            times: 2
    - service: remote_1code
      variables:
        rc_code_1: int
      then:
      - remote_transmitter.transmit_pioneer:
          rc_code_1: !lambda 'return rc_code_1;'
          repeat:
            times: 2
remote_transmitter:
  - id: ir_out
    pin: D2
    carrier_duty_percent: 50%
```
| Hex Code | Function |
|---|------|
| 0x5E13 | Input DVR |
| 0x5E15 | Input CD (XBOX) |
| 0x5E16 | Input Tuner |
| 0x5E1A | Vol Up |
| 0x5E1B | Vol Down |
| 0x5E1C | Mute |
| 0x5E54 | Input DTV/CABLE |
| 0x5E55 | Input V-Aux |
| 0x5E56 | Straight 5 |
| 0x5E57 | Sleep mode |
| 0x5E58 | Program > 1 |
| 0x5E59 | Program < 2 |
| 0x5E6A | Level Up |
| 0x5E6B | Level Down |
| 0x5E84 | Menu |
| 0x5E86 | Level |
| 0x5E87 | Input Multi-Channel 9 |
| 0x5E88 | Program Music |
| 0x5E89 | Program Entertain |
| 0x5E8A | Program Movie |
| 0x5E8B | Program Stereo |
| 0x5E8D | Program Sur. Decode |
| 0x5E94 | Enhancer 3 |
| 0x5E95 | Night 7 |
| 0x5E9C | Down |
| 0x5E9D | Up |
| 0x5E9E | Right |
| 0x5E9F | Left |
| 0x5EC1 | Input DVD |
| 0x5EC3 | Audio Sel 0 |
| 0x5EC9 | Input MD/CD-R |
| 0x5EDF | Diagnostics |
| 0x7E7E | Power On |
| 0x7E7F | Power Off |
