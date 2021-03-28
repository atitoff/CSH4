# Команды DALI

## Вариант 1

| #        | Command Code          | Repeat<br>< 100 ms | Answer<br>Slave | Command Name                          |  | 
| -------- | --------------------- | ------------------ | --------------- | ------------------------------------- | ---- |
| \-       | `YAAA AAA0 XXXX XXXX` |                    |                 | DIRECT ARC POWER CONTROL              | Установить яркость светильника с адресом 0AAA AAA или группы светильников с адресом 100A AAA <br>равной значению XXXX XXXX в течение FADE TIME |
| 0        | `YAAA AAA1 0000 0000` |                    |                 | OFF                                   | Выключить светильник с адресом AAA AAA или группу светильников с адресом 100A AAA                                                                                                           |
| 1        | `YAAA AAA1 0000 0001` |                    |                 | UP                                    | Увеличивать яркость светильника с адресом 0AAA AAA или группы<br>светильников с адресом 100A AAA в течение 200 мс со скоростью FADE RATE                                                    |
| 2        | `YAAA AAA1 0000 0010` |                    |                 | DOWN                                  | Уменьшать яркость светильника с адресом 0AAA AAA или группы<br>светильников с адресом 100A AAA в течение 200 мс со скоростью FADE RATE                                                      |
| 3        | `YAAA AAA1 0000 0011` |                    |                 | STEP UP                               | Увеличить яркость светильника с адресом 0AAA AAA или группы<br>светильников с адресом 100A AAA на один шаг                                                                                  |
| 4        | `YAAA AAA1 0000 0100` |                    |                 | STEP DOWN                             | Уменьшить яркость светильника с адресом 0AAA AAA<br>или группы светильников с адресом 100A AAA на один шаг                                                                                  |
| 5        | `YAAA AAA1 0000 0101` |                    |                 | RECALL MAX LEVEL                      | Установить яркость светильника с адресом 0AAA AAA или группы<br>светильников с адресом 100A AAA на уровень MAX\_LEVEL                                                                       |
| 6        | `YAAA AAA1 0000 0110` |                    |                 | RECALL MIN LEVEL                      | Установить яркость светильника с адресом 0AAA AAA или группы<br>светильников с адресом 100A AAA на уровень MIN\_LEVEL                                                                       |
| 7        | `YAAA AAA1 0000 0111` |                    |                 | STEP DOWN AND OFF                     | Уменьшить яркость светильника с адресом 0AAA AAA или группы<br>светильников с адресом 100A AAA на один шаг, если яркость на<br>уровне MIN\_LEVEL – выключить светильник                     |
| 8        | `YAAA AAA1 0000 1000` |                    |                 | ON AND STEP UP                        | Увеличить яркость светильника с адресом 0AAA AAA или группы<br>светильников с адресом 100A AAA на один шаг, если светильник<br>выключен – установить яркость на уровне MIN\_LEVEL           |
| 9-15     | `YAAA AAA1 0000 1XXX` |                    |                 | RESERVED                              |                                                                                                                                                                                             |
| 16-31    | `YAAA AAA1 0001 XXXX` |                    |                 | GO TO SCENE                           | Светильнику с адресом 1AAA AAA или группе светильников с<br>адресом 100А ААА перейти к сцене XXXX                                                                                           |
| 32       | `YAAA AAA1 0010 0000` | yes                |                 | RESET                                 |                                                                                                                                                                                             |
| 33       | `YAAA AAA1 0010 0001` | yes                |                 | STORE ACTUAL LEVEL IN THE DTR         |                                                                                                                                                                                             |
| 34 - 41  | `YAAA AAA1 0010 XXXX` |                    |                 | RESERVED                              |                                                                                                                                                                                             |
| 42       | `YAAA AAA1 0010 1010` | yes                |                 | STORE THE DTR AS MAX LEVEL            | Светильнику с адресом 1AAA AAA или группе светильников с<br>адресом 100А ААА сохранить значение регистра DTR в качестве MAX\_LEVEL                                                          |
| 43       | `YAAA AAA1 0010 1011` | yes                |                 | STORE THE DTR AS MIN LEVEL            | Светильнику с адресом 1AAA AAA или группе светильников с<br>адресом 100А ААА сохранить значение регистра DTR в качестве MIN\_LEVEL                                                          |
| 44       | `YAAA AAA1 0010 1100` | yes                |                 | STORE THE DTR AS SYSTEM FAILURE LEVEL | Светильнику с адресом 1AAA AAA или группе светильников с<br>адресом 100А ААА сохранить значение регистра DTR в качестве SYSTEM\_FAILURE\_LEVEL                                              |
| 45       | `YAAA AAA1 0010 1101` | yes                |                 | STORE THE DTR AS POWER ON LEVEL       | Светильнику с адресом 1AAA AAA или группе светильников с<br>адресом 100А ААА сохранить значение регистра DTR в качестве POWER\_ON\_LEVEL                                                    |
| 46       | `YAAA AAA1 0010 1110` | yes                |                 | STORE THE DTR AS FADE TIME            | Светильнику с адресом 1AAA AAA или группе светильников с<br>адресом 100А ААА сохранить значение регистра DTR в качестве FADE\_TIME                                                          |
| 47       | `YAAA AAA1 0010 1111` | yes                |                 | STORE THE DTR AS FADE RATE            | Светильнику с адресом 1AAA AAA или группе светильников с<br>адресом 100А ААА сохранить значение регистра DTR в качестве FADE\_RATE                                                          |
| 48 - 63  | `YAAA AAA1 0011 XXXX` |                    |                 | RESERVED                              |                                                                                                                                                                                             |
| 64 - 79  | `YAAA AAA1 0100 XXXX` | yes                |                 | STORE THE DTR AS SCENE                | Светильнику с адресом 1AAA AAA или группе светильников с<br>адресом 100А ААА сохранить значение регистра DTR в качестве<br>уровня яркости для сцены XXXX                                    |
| 80 - 95  | `YAAA AAA1 0101 XXXX` | yes                |                 | REMOVE FROM SCENE                     | Светильнику с адресом 1AAA AAA исключить себя из сцены XXXX                                                                                                                                 |
| 96 - 111 | `YAAA AAA1 0110 XXXX` | yes                |                 | ADD TO GROUP                          | Светильнику с адресом 1AAA AAA войти в группу XXXX                                                                                                                                          |
| 112 -127 | `YAAA AAA1 0111 XXXX` | yes                |                 | REMOVE FROM GROUP                     | Светильнику с адресом 1AAA AAA исключить себя из группы XXXX                                                                                                                                |
| 128      | `YAAA AAA1 1000 0000` | yes                |                 | STORE DTR AS SHORT ADDRESS            | Светильнику с адресом 1AAA AAA установить себе значение из<br>регистра DTR в качестве нового короткого адреса                                                                               |
| 129 -143 | `YAAA AAA1 1000 XXXX` |                    |                 | RESERVED                              |                                                                                                                                                                                             |
| 144      | `YAAA AAA1 1001 0000` |                    | yes             | QUERY STATUS                          |                                                                                                                                                                                             |
| 145      | `YAAA AAA1 1001 0001` |                    | yes             | QUERY BALLAST                         |                                                                                                                                                                                             |
| 146      | `YAAA AAA1 1001 0010` |                    | yes             | QUERY LAMP FAILURE                    |                                                                                                                                                                                             |
| 147      | `YAAA AAA1 1001 0011` |                    | yes             | QUERY LAMP POWER ON                   |                                                                                                                                                                                             |
| 148      | `YAAA AAA1 1001 0100` |                    | yes             | QUERY LIMIT ERROR                     |                                                                                                                                                                                             |
| 149      | `YAAA AAA1 1001 0101` |                    | yes             | QUERY RESET STATE                     |                                                                                                                                                                                             |
| 150      | `YAAA AAA1 1001 0110` |                    | yes             | QUERY MISSING SHORT ADDRESS           |                                                                                                                                                                                             |
| 151      | `YAAA AAA1 1001 0111` |                    | yes             | QUERY VERSION NUMBER                  |                                                                                                                                                                                             |
| 152      | `YAAA AAA1 1001 1000` |                    | yes             | QUERY CONTENT DTR                     |
|          |                       |                    | yes             | query physical minimum level          |  
|  |  |  | yes   | query power failure              |  
|  |  |  | yes   | query actual level               |  
|  |  |  | yes   | query max level                  |  
|  |  |  | yes   | query min level                  |  
|  |  |  | yes   | query power on level             |  
|  |  |  | yes   | query system failure level       |  
|  |  |  | yes   | query fade time / fade rate      |  
|  |  |  | yes   | query scene level (scenes 0-15)  |  
|  |  |  | yes   | query groups 0-7                 |  
|  |  |  | yes   | query groups 8-15                |  
|  |  |  | yes   | query random address (high)      |  
|  |  |  | yes   | query random address (middle)    | 
|  |  |  | yes   | query random address (low)       |  
| 161  |  |  |  | terminate                        |  
|  |  |  |  | set data transfer register (dtr) |  
|  |  |  |  | initialise                       |  
|  |  |  |  | randomise                        |  
|  |  |  | yes   | compare                          |  
|  |  |  |  | withdraw                         |  
|  |  |  |  | set search address (high)        |  
|  |  |  |  | set search address (middle)      |  
|  |  |  |  | set search address (low)         |  
|  |  |  |  | program short address            |  
|  |  |  | yes   | verify short address             |  
|  |  |  | yes   | query short address              |  
|  |  |  |  | physical selection               |  
|  |  |  |  | enable device type x             |  


## Вариант 2


| Command                                | Opcode | Description                                                                                                                                                                                         |
| -------------------------------------- | ------ | ----------------------------|
| OUTPUT LEVEL INSTRUCTIONS              |
| OFF                                    | 0x00   | Switches off lamp(s)                                                                                                                                                                                |
| UP                                     | 0x01   | Increases lamp(s) illumination level                                                                                                                                                                |
| DOWN                                   | 0x02   | Decreases lamp(s) illumination level                                                                                                                                                                |
| STEP UP                                | 0x03   | Increases the target illumination level by 1                                                                                                                                                        |
| STEP DOWN                              | 0x04   | Decreases the target illumination level by 1                                                                                                                                                        |
| RECALL MAX LEVEL                       | 0x05   | Changes the current light output to the maximum level                                                                                                                                               |
| RECALL MIN LEVEL                       | 0x06   | Changes the current light output to the minimum level                                                                                                                                               |
| STEP DOWN AND OFF                      | 0x07   | If the target level is zero, lamp(s) are turned off; if the target level is between the min. and max. levels, decrease the target level by one; if the target level is max., lamp(s) are turned off |
| ON AND STEP UP                         | 0x08   | If the target level is zero, lamp(s) are set to minimum level; if target level is between min. and max. levels, increase the target level by one                                                    |
| ENABLE DAPC SEQUENCE                   | 0x09   | Indicates the start of DAPC (level) commands                                                                                                                                                        |
| GO TO LAST ACTIVE LEVEL(1)             | 0x0A   | Sets the target level to the last active output level                                                                                                                                               |
| GO TO SCENE                            | 0x10   | Sets a group of lamps to a predefined scene                                                                                                                                                         |
| CONFIGURATION INSTRUCTIONS             |
| DALI RESET                             | 0x20   | Configures all variables back to their Reset state                                                                                                                                                  |
| STORE ACTUAL LEVEL IN DTR0             | 0x21   | Stores the actual level value into Data Transfer Register 0 (DTR0)                                                                                                                                  |
| SAVE PERSISTENT VARIABLES<sup>(1)</sup>           | 0x22   | Stores all variables into Nonvolatile Memory (NVM)                                                                                                                                                  |
| SET OPERATING MODE DTR0<sup>(1)</sup>  | 0x23   | Sets the operating mode to the value listed in DTR0     |
| RESET MEMORY BANK DTR0<sup>(1)</sup>      | 0x24 | Resets the memory bank identified by DTR0 (memory bank must be implemented and unlocked)          |
| IDENTIFY DEVICE^               | 0x25 | Instructs a control gear to run an identification procedure                                       |
| SET MAX LEVEL DTR0             | 0x2A | Configures the control gear's maximum output level to the value stored in DTR0                    |
| SET MIN LEVEL DTR0             | 0x2B | Configures the control gear's minimum output level to the value stored in DTR0                    |
| SET SYSTEM FAILURE LEVEL DTR0  | 0x2C | Sets the control gear's output level in the event of a system failure to the value stored in DTR0 |
| SET POWER ON LEVEL DTR0        | 0x2D | Configures the output level upon power-up based on the value of DTR0                              |
| SET FADE TIME DTR0             | 0x2E | Sets the fade time based on the value of  DTR0                                                    |
| SET FADE RATE DTR0             | 0x2F | Sets the fade rate based on the value of DTR0                                                     |
| SET EXTENDED FADE TIME DTR0<sup>(1)</sup> | 0x30 | Sets the extended fade rate based on the value of DTR0; used when fade time = 0                   |
| SET SCENE                      | 0x40 | Configures scene 'x' based on the value of DTR0                                                   |
| REMOVE FROM SCENE              | 0x50 | Removes one of the control gears from a scene                                                     |
| ADD TO GROUP                   | 0x60 | Adds a control gear to a group                                                                    |
| REMOVE FROM GROUP              | 0x70 | Removes a control gear from a group                                                               |
| SET SHORT ADDRESS DTR0         | 0x80 | Sets a control gear's short address to the value of DTR0                                          |
| ENABLE WRITE MEMORY            | 0x81 | Allows writing into memory banks                                                                  |
| QUERY INSTRUCTIONS             |
| QUERY STATUS                   | 0x90 | Determines the control gear's status based on a combination of gear properties                    |
| QUERY CONTROL GEAR PRESENT     | 0x91 | Determines if a control gear is present                                                           |
| QUERY LAMP FAILURE             | 0x92 | Determines if a lamp has failed                                                                   |
| QUERY LAMP POWER ON            | 0x93 | Determines if a lamp is On                                                                        |
| QUERY LIMIT ERROR              | 0x94 | Determines if the requested target level has been modified due to max. or min. level limitations  |
| QUERY RESET STATE                               | 0x95 | Determines if all NVM variables are in their Reset state                                                             |
| QUERY MISSING SHORT ADDRESS                     | 0x96 | Determines if a control gear's address is equal to 0xFF                                                              |
| QUERY VERSION NUMBER                            | 0x97 | Returns the device's version number located in memory bank 0, location 0x16                                          |
| QUERY CONTENT DTR0                              | 0x98 | Returns the value of DTR0                                                                                            |
| QUERY DEVICE TYPE                               | 0x99 | Determines the device type supported by the control gear                                                             |
| QUERY PHYSICAL MINIMUM                          | 0x9A | Returns the minimum light output that the control gear can operate at                                                |
| QUERY POWER FAILURE                             | 0x9B | Determines if an external power cycle occurred                                                                       |
| QUERY CONTENT DTR1                              | 0x9C | Returns the value of DTR1                                                                                            |
| QUERY CONTENT DTR2                              | 0x9D | Returns the value of DTR2                                                                                            |
| QUERY OPERATING MODE<sup>(1)</sup>              | 0x9E | Determines the control gear's operating mode                                                                         |
| QUERY LIGHT SOURCE TYPE<sup>(1)</sup>           | 0x9F | Returns the control gear's type of light source                                                                      |
| QUERY ACTUAL LEVEL                              | 0xA0 | Returns the control gear's actual power output level                                                                 |
| QUERY MAX LEVEL                                 | 0xA1 | Returns the control gear's maximum output setting                                                                    |
| QUERY MIN LEVEL                                 | 0xA2 | Returns the control gear's minimum output setting                                                                    |
| QUERY POWER ON LEVEL                            | 0xA3 | Returns the value of the intensity level upon power-up                                                               |
| QUERY SYSTEM FAILURE LEVEL                      | 0xA4 | Returns the value of the intensity level due to a system failure                                                     |
| QUERY FADE TIME FADE RATE                       | 0xA5 | Returns a byte in which the upper nibble is equal to the fade time value and the lower nibble is the fade rate value |
| QUERY MANUFACTURER SPECIFIC MODE<sup>(1)</sup>  | 0xA6 | Returns a 'YES' when the operating mode is within the range of 0x80 - 0xFF                                           |
| QUERY NEXT DEVICE TYPE<sup>(1)</sup>            | 0xA7 | Determines if the control gear has more than one feature, and if so, return the first/next device type or feature    |
| QUERY EXTENDED FADE TIME(1)   | 0xA8 | Returns a byte in which bits 6-4 is the value of the extended fade time multiplier and the lower nibble is the extended fade time base |
| QUERY CONTROL GEAR FAILURE(1) | 0xAA | Determines if a control gear has failed                                                                                                |
| QUERY SCENE LEVEL             | 0xB0 | Returns the level value of scene 'x'                                                                                                   |
| QUERY GROUPS 0-7              | 0xC0 | Returns a byte in which each bit represents a member of a group. A '1' represents a member of the group                                |
| QUERY GROUPS 8-15             | 0xC1 | Returns a byte in which each bit represents a member of a group. A '1' represents a member of the group                                |
| QUERY RANDOM ADDRESS H        | 0xC2 | Returns the upper byte of a randomly generated address                                                                                 |
| QUERY RANDOM ADDRESS M        | 0xC3 | Returns the high byte of a randomly generated address                                                                                  |
| QUERY RANDOM ADDRESS L        | 0xC4 | Returns the low byte of a randomly generated address                                                                                   |
| READ MEMORY LOCATION          | 0xC5 | Returns the content of the memory location stored in DTR0 that is located within the memory bank listed in DTR1                        |
| QUERY EXTENDED VERSION NUMBER | 0xFF | Returns the version number belonging to the device type or feature                                                                     |
| SPECIAL COMMANDS              |      |                                                                                                                                        |
| TERMINATE                     | 0xA1 | Stops the control gear's initialization                                                                                                |
| DTR0 DATA                     | 0xA3 | Loads a data byte into DTR0                                                                                                            |
| INITIALISE                    | 0xA5 | Initializes a control gear, command must be issued twice                                                                               |
| RANDOMIZE                     | 0xA7 | Generates a random address value, command must be issued twice                                                                         |
| COMPARE                       | 0xA9 | Compares the random address variable to the search address variable                                                                    |
| WITHDRAW                      | 0xAB | Changes the initialization state to reflect that a control gear had been identified but remains in the initialization state            |
| PING<sup>(1)</sup>            | 0xAD | Used by control devices to indicate theirm presence on the bus                                                                         |
| SEARCH ADDRH                  | 0xB1 | Determines if an address is present on the bus                                                                                         |
| SEARCH ADDRM                      | 0xB3 | Determines if an address is present on the bus                                        |
| SEARCH ADDRL                      | 0xB5 | Determines if an address is present on the bus                                        |
| PROGRAM SHORT ADDRESS             | 0xB7 | Programs a control gear's short address                                               |
| VERIFY SHORT ADDRESS              | 0xB9 | Verifies if a control gear's short address is correct                                 |
| QUERY SHORT ADDRESS               | 0xBB | Queries a control gear's short address                                                |
| ENABLE DEVICE TYPE                | 0xC1 | Enables a control gear's device type function                                         |
| DTR1 DATA                         | 0xC3 | Loads a data byte into DTR1                                                           |
| DTR2 DATA                         | 0xC5 | Loads a data byte into DTR2                                                           |
| WRITE MEMORY LOCATION             | 0xC7 | Writes data into a specific memory location and returns the value of the data written |
| WRITE MEMORY LOCATION NO REPLY(1) | 0xC9 | Writes data into a specific memory location but does not return a response            |


> Note 1: Addition commands introduced in DALI 2.0.

