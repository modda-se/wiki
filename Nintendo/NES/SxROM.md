# SxROM

**CHR-rom (27C1001-4001/27C010-0140)**

The following legs must be lifted and rewired since the eprom and the Nintendo PRG-rom chip isn't compatible.
1. Lift legs 1, 2, 22, 24, 30 and 31
2. Wire leg 1 & 31 to +5v (leg 32 on the eprom)
3. Wire leg 2 to the solder point under the lifted leg 24
4. Wire leg 22 to the solder point under the lifted leg 31
5. Wire leg 24 to the solder point under the lifted leg 2
6. Wire leg 30 to the solder point under the lifted leg 1

**PRG-rom (27C1001-4001/27C010-0140)**

The following legs must be lifted and rewired since the eprom and the Nintendo PRG-rom chip isn't compatible.
1. Lift legs 1, 2, 24, 30 and 31
2. Wire leg 1 to +5v (leg 32 on the eprom)
3. Wire leg 2 to the solder point under the lifted leg 24
4. Wire leg 24 to GND (leg 16 on the eprom)
5. Wire leg 30 to the solder point under the lifted leg 1
6. Wire leg 31 to the solder point under the lifted leg 2

## SL2ROM

**CHR-rom (27C1001-4001/27C010-040)**

Can be soldered as is, no changes needed.

**PRG-rom (27C1001-4001/27C010-040)**

The following legs must be lifted and rewired since the eprom and the Nintendo PRG-rom chip isn't compatible.
1. Lift legs 1, 2, 24, 30 and 31
2. Wire leg 1 & 24 to GND (leg 16 on the eprom)
3. Wire leg 2 to the solder point under the lifted leg 24
4. Leg 30 doesn't need to be conencted to anything
5. Wire leg 31 to +5v (leg 32 on the eprom)

*Note that there is three different types of MMC1*

- **MMC1A** = PRG RAM always on
- **MMC1B** = PRG RAM selectable on/off, default on
- **MMC1C** = PRG RAM selectable on/off, default off
