# Robbery Configuration

This configuration file defines the core settings for various robbery activities within the game, including debug options, different types of robberies, notification types, and police job configuration.

## Overview

The `Config` object controls the following settings:

- **Debug Mode**: Enables or disables debug features. print logs in f8
- **Robbery Types**: Configures which types of robberies are enabled (ATM, House, Jewelry, etc.).
- **Notification Type**: Defines the notification system used for in-game messages.
- **Police Jobs**: Configures which police jobs are considered as valid for police intervention during robberies.

### Debug Mode

 - **Enables or disables debug mode. When set to true, debug messages and logs will be shown to assist in troubleshooting and development. Set to false to disable debug features.**

```lua
Config.Debug = true
```

### Robbery Types

 - **Each robbery type corresponds to a specific in-game robbery activity. Setting each value to true enables that specific robbery type:**

   - **Config.ShopRobbery:** Enables robbery of shops (cash registers).
   - **Config.ATMRobbery:** Enables robbery of ATMs.
   - **Config.HouseRobbery:** Enables house robberies.
   - **Config.JewelryRobbery:** Enables jewelry store robberies.
   - **Config.SignRobbery:** Enables robbing signs (likely associated with stores or other locations).

**Set these to true to enable each robbery type or false to disable them.**

```lua
Config.ShopRobbery = true
Config.ATMRobbery = true
Config.HouseRobbery = true
Config.JewelryRobbery = true
Config.SignRobbery = true
```

### Notification Type

 - **NotificationType: Defines the notification system to use for in-game messages. Available options are:**

   - **'ox_lib':** Uses the ox_lib notification system for displaying messages.
   - **'esx':** Uses the esx notification system (for ESX framework-based servers).

```lua
Config.NotificationType = 'ox_lib' -- Options: 'ox_lib', 'esx'
```

### Police Jobs

- Police Jobs: They cannot start robbering and if you want to set up jobs that can respond to dispatch, look in cl_edit.lua

```lua
Config.PoliceJobs = { 
    ["police"] = true,
    ["sheriff"] = true,
}

```




# Shop Robbery

This configuration file defines the settings for robbing shops and safes in the game. Players can rob cash registers and safes, interact with objects, and receive rewards. The system includes settings for police intervention, robbery time, cooldowns, and skill checks required during the robbery.

## Overview

The `Config.Shop` object consists of two primary sections:

- **shops**: Settings related to robbing cash registers.
- **safes**: Settings related to robbing safes.

### Robbing Cash Register & Safe (Shops)

The configuration for robbing cash registers or safeincludes various settings for the robbery process, animation, and rewards.

```lua
Config.Shop = {
    shops = {
        Models = {'prop_till_01'}, -- Prop models for cash registers
        Label = 'Rob Cash Register',
        Icon = 'fa-solid fa-cash-register',
        Settings = {
            unlockItem = {'lockpick'}, -- Required item for robbing
            policeRequired = 0, -- Minimum police required online
            progressTime = 10000, -- Time to rob (in ms)
            CooldownTime = 600, -- Cooldown time for robberies in seconds
            rewardRange = {min = 1200, max = 3200}, -- Define range for dynamic reward
            rewardItem = 'money'
        },
        Animation = {
            scenario = 'PROP_HUMAN_PARKING_METER', -- Scenario to play while robbing
        },
        SkillCheck = {
            difficulty = {'easy', 'easy', {areaSize = 60, speedMultiplier = 2}, 'easy'},
            keys = {'w', 'a', 's', 'd'},
        },
    },
    safes = {
        locations = {
            vector3(-43.5469, -1748.5305, 29.4210),  -- Example coordinates for the first safe
            vector3(234.5, 678.9, 90.1),  -- Example coordinates for the second safe
            -- Add more safes with vector3 coordinates here
        },
        Label = 'Rob Safe',
        Icon = 'fa-solid fa-key',
        Settings = {
            unlockItem = {'lockpick'}, -- Required item for safes
            policeRequired = 0, -- Minimum police required online
            progressTime = 15000, -- Time to rob (in ms)
            radius = 2.0, -- Interaction radius for safes
            CooldownTime = 600, -- Cooldown time for robberies in seconds
            rewardRange = {min = 1200, max = 3200}, -- Define range for dynamic reward
            rewardItem = 'money'
        },
        Animation = {
            scenario = 'PROP_HUMAN_PARKING_METER', -- Scenario to play while robbing
        },
        SkillCheck = {
            difficulty = {'easy', 'easy', {areaSize = 40, speedMultiplier = 1.5}, 'easy'},
            keys = {'w', 'a', 's', 'd'},
        },
    },
}

```


# ATM Robbery 

This configuration file defines the settings and locations for robbing ATMs in the game. Players can use a specified item to unlock ATMs, complete the robbery process, and receive rewards. The system also includes settings for police intervention, cooldown, and reward range.

## Overview

The `Config.ATMs` object consists of:

- **Settings**: Customizable parameters that define how the ATM robbery system works.
- **Locations**: A list of coordinates where the ATMs are located, which players can rob.

### Settings

```lua
Config.ATMs = {
    Settings = {
        unlockItem = 'lockpick',           -- Item used to unlock the ATM
        progressTime = 3000,               -- Time to complete the robbery in milliseconds (3000ms = 3 seconds)
        rewardRange = {min = 1200, max = 3200}, -- The range for dynamic reward amounts (between min and max)
        policeRequired = 2,                -- Minimum number of police required to stop the robbery
        cooldown = 600,                    -- Cooldown time in seconds before the player can rob again (600s = 10 minutes)
        rewardItem = 'money'               -- Item given as a reward for completing the robbery (money in this case)
    },
    Locations = {
        {coords = vector3(33.2127, -1348.2249, 29.4970)},
        {coords = vector3(28.1395, -1339.157, 29.49702)},
        {coords = vector3(-3047.781, 585.554, 7.908927)},
        {coords = vector3(-3249.988, 1004.37, 12.83072)},
        {coords = vector3(1734.912, 6420.816, 35.03722)},
        {coords = vector3(1707.865, 4920.4, 42.06363)},
        {coords = vector3(1959.3, 3748.987, 32.34373)},
        {coords = vector3(546.4423, 2662.851, 42.15649)},
        {coords = vector3(2672.792, 3286.709, 55.24113)},
        {coords = vector3(2549.234, 384.8363, 108.6229)},
        {coords = vector3(378.1743, 333.3306, 103.5664)},
        {coords = vector3(-709.7484, -904.2379, 19.21558)}
    }
}
```





# Jewelry Robbery

This configuration file defines the settings, reward items, and locations for a jewelry heist system in a game. Players can rob jewelry showcases, receive random rewards based on defined chances, and face a cooldown and police requirements.

## Overview

The `Config.Jewelry` object consists of:

- **Settings**: Customizable parameters that define how the jewelry heist system works.
- **RewardItems**: A list of jewelry items that can be stolen, each with a chance and reward range.
- **Locations**: A set of coordinates where the jewelry showcases are located, where players can attempt to rob. **!! Don't change Type = "showcase" !!**

### Settings

```lua
Config.Jewelry = {
    Settings = {
        progressTime = 3000,             -- Time to complete the heist in milliseconds (3000ms = 3 seconds)
        policeRequired = 0,              -- Minimum number of police officers required to start the heist (0 = no police required)
        cooldown = 600,                  -- Cooldown time in seconds before a player can rob again (600s = 10 minutes)
        Delay = 60000 * 60               -- Time delay (1 hour in milliseconds)
    },
    RewardItems = {
        { Item = "bracelet", Chance = 25, Min = 6, Max = 15 },
        { Item = "gold_bracelet", Chance = 20, Min = 6, Max = 15 },
        { Item = "gold_watch", Chance = 10, Min = 6, Max = 15 },
        { Item = "rolex", Chance = 15, Min = 6, Max = 15 },
        { Item = "necklace", Chance = 30, Min = 9, Max = 15 }
    },
    Locations = {
        { Coords = vec3(-627.81, -234.12, 38.01), Type = "showcase" },
        { Coords = vec3(-626.75, -233.32, 38.06), Type = "showcase" },
        { Coords = vec3(-625.91, -234.43, 38.11), Type = "showcase" },
        { Coords = vec3(-624.21, -230.92, 38.06), Type = "showcase" },
        { Coords = vec3(-623.84, -228.38, 38.06), Type = "showcase" },
        { Coords = vec3(-621.23, -228.73, 38.06), Type = "showcase" },
        { Coords = vec3(-619.92, -230.57, 38.06), Type = "showcase" },
        { Coords = vec3(-620.27, -233.14, 38.06), Type = "showcase" },
        { Coords = vec3(-622.87, -232.78, 38.06), Type = "showcase" },
        { Coords = vec3(-620.08, -234.67, 38.06), Type = "showcase" },
        { Coords = vec3(-618.98, -233.88, 38.06), Type = "showcase" },
        { Coords = vec3(-617.35, -230.38, 38.06), Type = "showcase" },
        { Coords = vec3(-618.13, -229.32, 38.06), Type = "showcase" },
        { Coords = vec3(-619.49, -227.5, 38.06), Type = "showcase" },
        { Coords = vec3(-620.22, -226.42, 38.06), Type = "showcase" },
        { Coords = vec3(-624.08, -226.88, 38.06), Type = "showcase" },
        { Coords = vec3(-625.1, -227.61, 38.06), Type = "showcase" },
        { Coords = vec3(-625.48, -238.03, 38.06), Type = "showcase" },
        { Coords = vec3(-626.54, -238.77, 38.06), Type = "showcase" },
        { Coords = vec3(-627.01, -235.18, 38.06), Type = "showcase" }
    }
}
```






# Sign Robbery 

This configuration file defines the settings and models for a sign robbery system in a game. It allows players to rob signs for rewards, with customizable settings like item chances, progress time, and police notification. It also includes support for an anti-cheat system for automated bans when a player triggers an exploit.

## Overview

The `Config.SignRobbery` object consists of:

- **Settings**: Customizable parameters for the sign robbery system.
- **Models**: A list of models representing the types of signs available for robbery.

### Settings

```lua
Config.SignRobbery = {
    Settings = {
        scrapitem = 'lockpick',           -- Item used to start the robbery
        progressTime = 3000,              -- Time (in ms) to complete the robbery
        cooldown = 200,                   -- Cooldown time (in ms) after each robbery
        chancetocallpolice = 100,         -- Chance (in %) to call the police during the robbery
        rewardRange = {min = 3, max = 10},-- Range of the reward (randomly chosen between min and max)
        rewardItem = 'burger',            -- Item given as a reward for completing the robbery
        WayAnticheat = true               -- Enable anti-cheat system (true = with anti-cheat, false = without)
    },
    Models = {
        'prop_sign_road_01a',
        'prop_sign_road_05a',
        'prop_sign_road_03e',
        'prop_sign_road_03m',
        'prop_sign_road_04a',
        'prop_sign_road_05e',
        'prop_sign_road_05e',
        'prop_sign_road_restriction_10',
        'prop_sign_road_02a',
        'prop_sign_road_03g'
    }
}
```







# House Robbery

This configuration file defines the settings and locations for house robberies in the game. Players can rob houses, interact with different rooms, and receive random items as rewards. The system includes settings for police intervention, the chances of police being called, and the list of items that may be obtained during the robbery.

## Overview

The `Config.Houses` object consists of:

- **HousesSetings**: Global settings for police intervention and chances of calling the police.
- **Houses**: A list of house configurations, each with defined doors, interiors, and rooms containing items.

### Houses Config
         - not the same in config in config.lua

```lua

Config.HousesSetings = {
    chancetocallpolice = 100, -- This setting indicates the probability or chance of calling the police, with a value of 100 likely meaning a guaranteed chance, or a 100% chance.
    policeRequired = 2 -- This setting defines the number of police officers required for a specific action or event to occur, with a value of 2 indicating two officers are needed.
}

Config.Houses = {
    House1 = {
        Door = vec3(-66.6089, 489.9209, 144.8848), 
        Interior = vec3(-174.3378, 497.484, 137.6535),
        Bucket = math.random(1, 999999),
        Location = {
            ['1'] = {
                coords = vec3(-165.6677, 495.7021, 133.8560),
                Items = {
                    ['burger'] = {label = 'Burger', chance = 40, amount = {1, 3}},
                    ['radio'] = {label = 'Radio', chance = 15, amount = {1, 1}},
                    ['burger'] = {label = 'Burger', chance = 15, amount = {1, 3}},
                    ['phone'] = {label = 'Phone', chance = 15, amount = {1, 1}},
                    ['WEAPON_PISTOL'] = {label = 'Pistol', chance = 10, amount = {1, 1}},
                    ['WEAPON_SAWNOFFSHOTGUN'] = {label = 'Sawnoff Shotgun', chance = 5, amount = {1, 1}}
                }
            },
            ['2'] = {
                coords = vec3(-163.1815, 484.9880, 133.8696),
                Items = {
                    ['burger'] = {label = 'Cola', chance = 30, amount = {1, 2}},
                    ['radio'] = {label = 'Radio', chance = 10, amount = {1, 1}},
                    ['phone'] = {label = 'Phone', chance = 10, amount = {1, 1}},
                    ['WEAPON_KNIFE'] = {label = 'Knife', chance = 5, amount = {1, 1}}
                }
            }
        }
    }
}



```
**Check template.md**



This `readme.md` should help you understand the purpose and settings of our configuration, as well as how to modify and use it within a game or server environment.
