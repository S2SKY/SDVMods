﻿### Requirements
- SMAPI 2.5+
- Stardew Valley 1.2.33

### This Mod Does:
- Going out in storms, blizzards, frosts and heatwaves is now more perilous, as it drains your stamina. Thankfully, 
    a 'Muscle Remedy' has been found to cure even the hardiest flu

### Stamina System

__Very Important: Read this before you alter StaminaDrain in the config!__

Rather than a fixed penalty for certain conditions, this now calculates a multiplier based on the conditions prevailing.

Every ten minutes, the mod checks to see if you've been outside for a certain percentage of the last 10 minutes. By default, it's set to 65%. (This percentage is calculated by counting the ticks you've been outside and the total number in the span to account for time change mods). Then, it generates a random number and tests it against a chance to get sick. By default, this is 70%. In addition, this must be during certain weather conditions:
*Temperature: Frost or Heatwave (as defined in the config file, see the readme for more information)
*Weathers: Lightning
*Special Weathers: Thundersnow, Blizzard
(NB: While you incur a stamina penalty for being sick in fog, it deliberately does not trigger this.)

The penalties are **cumulative** - that is, they add up to the final multiplier.
*Lightning : +100% ( 1)
*Thundersnow: +100% (1)
*Thundersnow (nighttime): +50% (.5)
*Foggy: +50% (.5)
*Foggy (nightime) +25% (.25)
*Blizzard: +125% (1.25)
*Blizzard: **White Out**+245% (2.45)
*Thunder Frenzy: +185% (1.85)
*Blizzard (nighttime) +50% (.5)
*Frost (nightime): +125% (1.25) - this is not during the winter. During winter, the frost penalty is untriggered.
*Heatwave (daytime): +125% (1.25)

The calculated number is then rounded __down__

For example, therefore, if you're outduring a storm, with the base of 2, you only take a stamina penalty of 2. But if it's also a heatwave, your penatly is now (+1+1.25)=*2.25 or 4.5. So a penalty of 4.
If you're out in a blizzard during the day, it's *1.25 or 2.5 rounded down to 2. If you're out in that blizzard at night, another .5 (1.25+.5) is added making it 1.75 or 3.5 rounded down to 3.

(This does mean a foggy blizzard at night is (+.5+.25+1.25+.5 or *2.25), and if you somehow get this in fall, would be *3.5. And somehow, if you get a whiteout, it would be *3.25 and *4.5!)

### Options Config

- `AffectedOutside` - The percentage outside you need to be within a 10 minute span to be affected by stamina events.
 Defaults to '.65', valid values are between 0 and 1. To turn stamina drains off entirely, set it to 0. Do not recommend setting to 1.

 - `SickMoreThanOnce` - This setting controls whether or not you can get sick once you have cured yourself. Default: `false`. Valid: `true, false`

 - `StaminaDrain` - This is an int containing the default stamina drain for hazardous events. See the writeup (soon) for more information. Default is '2'. Valid range is any number between foo and bar.'

  - `ChanceOfGettingSick` - Controls the chance you'll get sick when conditions are matched. Default is set to '.7' for (70% chance). Valid Range is 0 to 1.