# The capship brain

## Analysis

### Pseudocode

```
for every ship with a brain
   if the ship is still alive and in mission
      if the ship is a Hyperion
         if it is between 100 and 75% of health or has 1 simulated health
            apply Heavy Armor 60
            for turret03 through turret15
               set fire rate to 120%
            every 10 seconds
               do not repair hull
               repair live subsystems by 1%
               do not repair dead subsystems
               do not repair live turrets 
               do not repair dead turrets
               if the weapons subsystem is alive
                  create a Cruiser Flare
               if engines are alive
                  set thrusters to on
               if the player is targeting the ship
                  activate custom hud gauges
                  set text to "GTC Hyperion // Reactor Rating 12 // ***Weapons 120% // *** Armor 40% // ** Repairs // Maneuvering Std"
                  if the Navigation subsystem has Cargo named "Charged"
                     Add text "DRIVE CHARGED // *** Jump Cycle 5m"
                  Add text "ECM Std"
               Set ship flags
                  "friendly-stealth-invisible" true
                  "free-afterburner-use" false
                  "primaries-locked" false
               if global difficulty level is at least "Hard" and the ship does not have the "secondaries-locked" flag
                  for every subsystem and turret
                     apply Light Armor 80
               for turret01 and turret02
                  apply subsys-guardian with threshold 15
                  if the turret has less than 16% health left and carries cargo named "Nothing"
                     lock the turret
                     set turret cargo to "Shuttered"
                     set subsystem name to "SHUTTERED"
                  if the turret has more than 33% health and has cargo "Shuttered"
                     unlock turret
                     set turret cargo to "Nothing"
                     set subsystem name to "Beam Cannon"
                  if the ship carries cargo named "Shuttered"
                     every 3 seconds
                        repair the subsystem by 1%
               if the weapon energy is at 100% 
                  if Navigation subsystem carries neither "Charged" nor "Charging" cargo
                     set ets to 12/0/0
                     set weapon energy to 0
                     set Navigation cargo to "Charging"
                  if Navigation subsystem carries "Charging" cargo
                     every 6 seconds
                        set Navigation cargo to "Charged"
               if weapon energy is below 100%
                  if Navigation subsystem does not carry "Charged" cargo
                     every 6 seconds
                        increase weapon energy by 2%
            if it is between 75 and 35% health or has 2 simulated health
               apply Heavy Armor 40
               for turret03 through turret15
                  set fire rate to 100%
               every 10 seconds
                  repair hull by 1%
                  repair live subsystems by 1%
                  if a subsystem is dead
                     if mission time mod 60 is between 0 and 2
                        repair subsystem by 15%
                  for every turret
                     every 10 seconds
                        if the turret has more than 1% health remaining
                           if the turret does not carry the "Knocked Out" cargo
                              repair the turret by 1%
                           if the turret is dead
                              do not repair
               if engines are alive
                  set thrusters to on
               every 9 to 11 seconds
                  if the weapons subsystem has health remaining
                     create a Cruiser Flare
               if the player is targeting the ship
                  activate custom hud gauges
                  set text to "GTC Hyperion // Reactor Rating 12 // ** Weapons 100% // ***** Armor 60% // *** Repairs // * Maneuvering Std // * Jump Cycle 20m // ECM Std"
               Set ship flags
                  "friendly-stealth-invisible" true
                  "free-afterburner-use" true
                  "primaries-locked" false
               if global difficulty level is at least "Hard" and the ship does not have the "secondaries-locked" flag
                  for every subsystem and turret
                     apply Light Armor 60
               for turret01 and turret02
                  apply subsys-guardian with threshold 15
                  if the turret has less than 16% health left and carries cargo named "Nothing"
                     lock the turret
                     set ship cargo to "Shuttered"
                     set subsystem name to "SHUTTERED"
                  if the turret has more than 33% health and has cargo "Shuttered"
                        unlock turret
                        set turret cargo to "Nothing"
                        set subsystem name to "Beam Cannon"
                    if the turret carries cargo named "Shuttered"
                        every 3 seconds
                           repair the subsystem by 1%
                           if the weapon energy is at 100% 
               if the weapon energy is at 100% 
                  if Navigation subsystem carries neither "Charged" nor "Charging" cargo
                     set ets to 12/0/0
                     set weapon energy to 0
                     set Navigation cargo to "Charging"
                  if Navigation subsystem carries "Charging" cargo
                     every 6 seconds
                        set Navigation cargo to "Charged"
               if weapon energy is below 100%
                  if Navigation subsystem does not carry "Charged" cargo
                     every 6 seconds
                        increase weapon energy by 2%
            if it is between 35 and 0% health or has 3 simulated health
               apply heavy armor 60
               for turret03 through turret15
                  set fire rate to 50%
               every 10 seconds
                  repair hull by 1%
                  repair live subsystems by 2%
                  repair live turrets by 1%
                  do not repair dead subsystems
               every 57 to 63 seconds
                  repair dead subsystem by 15%
               if engines are alive
                  set thrusters to on
               every 9 to 11 seconds
                  if the weapon subsystem is alive
                     create a cruiser flare
               if the player is targeting the ship
                  activate custom hud gauges
                  set text to "GTC Hyperion // Emergency Power // - Weapons 50% // ***** Armor 60% // *** Repairs // * Maneuvering Std // ***** Jump Cycle 2.5m // ECM Std"
               Set ship flags
                  "friendly-stealth-invisible" false
                  "free-afterburner-use" false
                  "primaries-locked" true
               if global difficulty level is at least "Hard" and the ship does not have the "secondaries-locked" flag
                  for every subsystem and turret
                     apply Light Armor 60
               for turret01 and turret02
                  apply subsys-guardian with threshold 15
                  if the turret has less than 16% health left and carries cargo named "Nothing"
                     lock the turret
                     set turret cargo to "Shuttered"
                     set subsystem name to "SHUTTERED"
                  if the turret has more than 33% health and has cargo "Shuttered"
                     unlock turret
                     set ship cargo to "Nothing"
                     set subsystem name to "Beam Cannon"
                  if the turret carries cargo named "Shuttered"
                     every 3 seconds
                        repair the subsystem by 1%
               if the weapon energy is at 100% 
                  if Navigation subsystem carries neither "Charged" nor "Charging" cargo
                     set ets to 12/0/0
                     set weapon energy to 0
                     set Navigation cargo to "Charging"
                  if Navigation subsystem carries "Charging" cargo
                     every 6 seconds
                        set Navigation cargo to "Charged"
               if weapon energy is below 100%
                  if Navigation subsystem does not carry "Charged" cargo
                     every 6 seconds
                        increase weapon energy by 2%
```              

## LUA interface

The following sexps need to be created to allow mission designers to control brains:
* `brain-activate` _shipname_ 
   activates brain activity for the given ship if the ship class has a brain config
* `brain-deactivate` _shipname_
   turns the brain off
* `brain-force-behaviour` _shipname_ (high health | mid health | low health)
   Forces a ship to use a given behaviour pattern regardless of actual health
* `brain-get-behaviour-state` _shipname_
   Returns (high health | mid health | low health)
* `brain-get-drive-state` _shipname_
   Returns (Charging | Charged)
* `brain-get-weapon-state` _shipname_
   Returns current weapon fire rate
* `brain-get-repair-state` _shipname_
   Returns current state of the repair system

## Configuration file (draft)

Configuration should be done in a table-like format.
Draft format:
```
$Class: GTC Hyperion
   $Beam turrets: [List of beam turrets. These will use the "Shutter" behaviour]
   $Enable Knockout For: [List of subsystems. These will not be regenerated once knocked out]

   $High health bracket: <upper bound> <lower bound>  // Analoguous entries exist for Med and low health
      +Hull Armor: <Armortype>                        // This armor type will be applied when the ship is in this state
      +Subsystem Armor: <Armortype>                   // Apply this armor to all non-turret subsystems
      +Turret Armor: <Armortype>                      // Apply this armor to all turrets
      +Hull Repair: <integer>                         // Hull regenerates by this percentage every tick
      +Hull Repair Tickrate: <integer>                // Time in seconds to apply a health regen 
      +Hull Repair Tickrate Variance: <integer>       // Vary the tick time by this amount after every tick
      +Subsystem Repair: <integer>                    // follows the above        
      +Subsystem Repair Tickrate: <integer>
      +Subsystem Repair Tickrate Variance: <integer>
      +Dead Subsystem Repair: <integer>
      +Dead Subsystem Repair Tickrate: <integer>
      +Dead Subsystem Repair Tickrate Variance: <integer>
      +Turret Repair: <integer>   
      +Turret Repair Tickrate: <integer>
      +Turret Repair Tickrate Variance: <integer>
      +Dead Turret Repair: <integer>
      +Dead Turret Repair Tickrate: <integer>
      +Dead Turret Repair Tickrate Variance: <integer>
      +Jump Charge Rate: <integer>                   
      +Jump Charge Tickrate: <integer>
      +Jump Charge Tickrate Variance: <integer>
      +Flares: <boolean>                              // If true, fire flares according to tickrate
         +Flare tick rate: <integer>                  
         +Flare type: <Countermeasure type>
         +Subsystem: <Subsystem to track>             // Flares will only fire as long as this subsystem is alive

      +Difficulty: Hard                               // variant settings based on difficulty level. Every setting from above can be repeated here.
         +Subsystem Armor: Light Armor 80
         +Turret Armor: Light Armor 80
```



## Raw sexp code

```
$Formula: ( when-argument 
   ( any-of 
      "Diomedes" 
      "Hyperion B" 
      "Hyperion C" 
      "Hyperion" 
      "Erebus" 
   )
   ( not 
      ( destroyed-or-departed-delay 
         0 
         "<argument>" 
      )
   )
   ( do-nothing ) 
   ( when 
      ( is-ship-class 
         "GTC Hyperion" 
         "<argument>" 
      )
      ( when 
         ( or 
            ( and 
               ( <= ( hits-left "<argument>" ) 100 ) 
               ( > ( hits-left "<argument>" ) 75 ) 
            )
            ( = ( sim-hits-left "<argument>" ) 1 ) 
         )
         ( when 
            ( true ) 
            ( set-armor-type 
               "<argument>" 
               ( true ) 
               "Heavy Armor 60" 
               "Hull" 
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "<argument>" 
         )
         ( when-argument 
            ( every-of 
               "turret03" 
               "turret04 " 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
            )
            ( true ) 
            ( turret-set-rate-of-fire 
               "@shipNameHolder[noname]" 
               120 
               "<argument>" 
            )
         )
         ( when-argument 
            ( any-of "Hull" ) 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  100 
               )
               ( > 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when 
            ( not 
               ( < 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Engines" 
                  )
                  1 
               )
            )
            ( set-thrusters-status 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( > 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Weapons" 
                  )
                  0 
               )
               ( is-in-mission "<argument>" ) 
            )
            ( weapon-create 
               "<argument>" 
               "Cruiser Flare" 
               ( get-object-x "<argument>" "Engine" ) 
               ( get-object-y "<argument>" "Engine" ) 
               ( get-object-z "<argument>" "Engine" ) 
               ( get-object-pitch "<argument>" ) 
               ( get-object-bank "<argument>" ) 
               ( get-object-heading "<argument>" ) 
            )
         )
         ( when 
            ( and 
               ( true ) 
               ( targeted "<argument>" ) 
               ( targeted "<argument>" ) 
            )
            ( hud-set-custom-gauge-active 
               ( true ) 
               "BPLowerRightMFD" 
               "BPLowerRightMFDA" 
               "BPLowerRightMFDB" 
               "BPLowerRightMFDC" 
               "BPLowerRightMFDD" 
               "BPLowerRightMFDE" 
               "BPLowerRightMFDF" 
               "BPLowerRightMFDG" 
               "BPLowerRightMFDH" 
            )
            ( hud-set-text 
               "BPLowerRightMFD" 
               "GTC Hyperion" 
            )
            ( hud-set-text 
               "BPLowerRightMFDA" 
               "Reactor Rating 12" 
            )
            ( hud-set-text 
               "BPLowerRightMFDB" 
               "*** Weapons 120%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDC" 
               "*** Armor 40%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDD" 
               "** Repairs" 
            )
            ( hud-set-text 
               "BPLowerRightMFDE" 
               "* Maneuvering Std" 
            )
            ( if-then-else 
               ( is-cargo 
                  "Charged" 
                  "<argument>" 
                  "Navigation" 
               )
               ( hud-set-text 
                  "BPLowerRightMFDF" 
                  "DRIVE CHARGED" 
               )
               ( hud-set-text 
                  "BPLowerRightMFDF" 
                  "*** Jump Cycle 5m" 
               )
            )
            ( hud-set-text 
               "BPLowerRightMFDG" 
               "ECM Std" 
            )
         )
         ( when 
            ( true ) 
            ( alter-ship-flag 
               "friendly-stealth-invisible" 
               ( true ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "free-afterburner-use" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "primaries-locked" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( skill-level-at-least "Hard" ) 
               ( not 
                  ( are-ship-flags-set 
                     "<argument>" 
                     "secondaries-locked" 
                  )
               )
            )
            ( when-argument 
               ( every-of 
                  "Weapons" 
                  "Communication" 
                  "Communications" 
                  "Sensors" 
                  "Reactor" 
                  "Engine" 
                  "Engine01" 
                  "Engine02" 
                  "Engine03" 
                  "Engine04" 
                  "Navigation" 
                  "turret01" 
                  "turret02" 
                  "turret03" 
                  "turret04" 
                  "turret05" 
                  "turret06" 
                  "turret07" 
                  "turret08" 
                  "turret09" 
                  "turret10" 
                  "turret11" 
                  "turret12" 
                  "turret13" 
                  "turret14" 
                  "turret15" 
                  "turret16" 
                  "turret17" 
                  "turret18" 
                  "turret19" 
                  "turret20" 
                  "turret21" 
                  "turret22" 
                  "turret23" 
                  "turret24" 
                  "turret25" 
                  "turret26" 
                  "turret27" 
                  "turret28" 
                  "turret29" 
                  "turret30" 
                  "turret31" 
                  "turret32" 
                  "turret33" 
                  "turret34" 
                  "turret35" 
                  "turret36" 
                  "turret37" 
                  "turret38" 
                  "turret39" 
                  "turret40" 
                  "turret41" 
                  "turret42" 
                  "turret43" 
                  "turret44" 
                  "turret45" 
                  "turret46" 
                  "turret47" 
                  "turret48" 
                  "turret49" 
                  "turret50" 
               )
               ( true ) 
               ( set-armor-type 
                  "@shipNameHolder[noname]" 
                  ( true ) 
                  "Light Armor 80" 
                  "<argument>" 
               )
            )
         )
         ( when-argument 
            ( any-of "turret01" "turret02" ) 
            ( true ) 
            ( ship-subsys-guardian-threshold 
               15 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     16 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Shuttered" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "SHUTTERED" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     33 
                  )
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Beam Cannon" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( repair-subsystem 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
                  1 
               )
            )
         )
         ( when 
            ( true ) 
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( or 
                        ( is-cargo 
                           "Charged" 
                           "<argument>" 
                           "Navigation" 
                        )
                        ( is-cargo 
                           "Charging" 
                           "<argument>" 
                           "Navigation" 
                        )
                     )
                  )
               )
               ( set-ets-values 12 0 0 "<argument>" ) 
               ( set-weapon-energy 0 "<argument>" ) 
               ( set-cargo 
                  "Charging" 
                  "<argument>" 
                  "Navigation" 
               )
            )
            ( when 
               ( and 
                  ( < 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( is-cargo 
                        "Charged" 
                        "<argument>" 
                        "Navigation" 
                     )
                  )
                  ( = ( mod ( mission-time ) 6 ) 0 ) 
               )
               ( set-weapon-energy 
                  ( + 
                     ( weapon-energy-pct "<argument>" ) 
                     2 
                  )
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( is-cargo 
                     "Charging" 
                     "<argument>" 
                     "Navigation" 
                  )
                  ( = ( mod ( mission-time ) 6 ) 0 ) 
               )
               ( set-cargo 
                  "Charged" 
                  "<argument>" 
                  "Navigation" 
               )
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noname" 
         )
      )
      ( when 
         ( or 
            ( and 
               ( <= ( hits-left "<argument>" ) 75 ) 
               ( > ( hits-left "<argument>" ) 35 ) 
            )
            ( = ( sim-hits-left "<argument>" ) 2 ) 
         )
         ( set-armor-type 
            "<argument>" 
            ( true ) 
            "Heavy Armor 40" 
            "Hull" 
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "<argument>" 
         )
         ( when-argument 
            ( every-of 
               "turret03" 
               "turret04 " 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
            )
            ( true ) 
            ( turret-set-rate-of-fire 
               "@shipNameHolder[noname]" 
               100 
               "<argument>" 
            )
         )
         ( when-argument 
            ( any-of "Hull" ) 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  100 
               )
               ( > 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 5 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = 
                  ( mod ( mission-time ) 60 ) 
                  ( rand-multiple 0 2 ) 
               )
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               15 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
               ( not 
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when 
            ( not 
               ( < 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Engines" 
                  )
                  1 
               )
            )
            ( set-thrusters-status 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( = 
                  ( mod 
                     ( mission-time ) 
                     ( rand-multiple 9 11 ) 
                  )
                  0 
               )
               ( > 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Weapons" 
                  )
                  0 
               )
               ( is-in-mission "<argument>" ) 
            )
            ( weapon-create 
               "<argument>" 
               "Cruiser Flare" 
               ( get-object-x "<argument>" "Engine" ) 
               ( get-object-y "<argument>" "Engine" ) 
               ( get-object-z "<argument>" "Engine" ) 
               ( get-object-pitch "<argument>" ) 
               ( get-object-bank "<argument>" ) 
               ( get-object-heading "<argument>" ) 
            )
         )
         ( when 
            ( and 
               ( true ) 
               ( targeted "<argument>" ) 
               ( targeted "<argument>" ) 
            )
            ( hud-set-custom-gauge-active 
               ( true ) 
               "BPLowerRightMFD" 
               "BPLowerRightMFDA" 
               "BPLowerRightMFDB" 
               "BPLowerRightMFDC" 
               "BPLowerRightMFDD" 
               "BPLowerRightMFDE" 
               "BPLowerRightMFDF" 
               "BPLowerRightMFDG" 
               "BPLowerRightMFDH" 
            )
            ( hud-set-text 
               "BPLowerRightMFD" 
               "GTC Hyperion" 
            )
            ( hud-set-text 
               "BPLowerRightMFDA" 
               "Reactor Rating 12" 
            )
            ( hud-set-text 
               "BPLowerRightMFDB" 
               "** Weapons 100%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDC" 
               "***** Armor 60%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDD" 
               "*** Repairs" 
            )
            ( hud-set-text 
               "BPLowerRightMFDE" 
               "* Maneuvering Std" 
            )
            ( hud-set-text 
               "BPLowerRightMFDF" 
               "* Jump Cycle 20m" 
            )
            ( hud-set-text 
               "BPLowerRightMFDG" 
               "ECM Std" 
            )
         )
         ( when 
            ( true ) 
            ( alter-ship-flag 
               "friendly-stealth-invisible" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "free-afterburner-use" 
               ( true ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "primaries-locked" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( skill-level-at-least "Hard" ) 
               ( not 
                  ( are-ship-flags-set 
                     "<argument>" 
                     "secondaries-locked" 
                  )
               )
            )
            ( when-argument 
               ( every-of 
                  "Weapons" 
                  "Communication" 
                  "Communications" 
                  "Sensors" 
                  "Reactor" 
                  "Engine" 
                  "Engine01" 
                  "Engine02" 
                  "Engine03" 
                  "Engine04" 
                  "Navigation" 
                  "turret01" 
                  "turret02" 
                  "turret03" 
                  "turret04" 
                  "turret05" 
                  "turret06" 
                  "turret07" 
                  "turret08" 
                  "turret09" 
                  "turret10" 
                  "turret11" 
                  "turret12" 
                  "turret13" 
                  "turret14" 
                  "turret15" 
                  "turret16" 
                  "turret17" 
                  "turret18" 
                  "turret19" 
                  "turret20" 
                  "turret21" 
                  "turret22" 
                  "turret23" 
                  "turret24" 
                  "turret25" 
                  "turret26" 
                  "turret27" 
                  "turret28" 
                  "turret29" 
                  "turret30" 
                  "turret31" 
                  "turret32" 
                  "turret33" 
                  "turret34" 
                  "turret35" 
                  "turret36" 
                  "turret37" 
                  "turret38" 
                  "turret39" 
                  "turret40" 
                  "turret41" 
                  "turret42" 
                  "turret43" 
                  "turret44" 
                  "turret45" 
                  "turret46" 
                  "turret47" 
                  "turret48" 
                  "turret49" 
                  "turret50" 
               )
               ( true ) 
               ( set-armor-type 
                  "@shipNameHolder[noname]" 
                  ( true ) 
                  "Light Armor 60" 
                  "<argument>" 
               )
            )
         )
         ( when-argument 
            ( any-of "turret01" "turret02" ) 
            ( true ) 
            ( ship-subsys-guardian-threshold 
               15 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     16 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Shuttered" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "SHUTTERED" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     33 
                  )
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Beam Cannon" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( repair-subsystem 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
                  1 
               )
            )
         )
         ( when 
            ( true ) 
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( or 
                        ( is-cargo 
                           "Charged" 
                           "<argument>" 
                           "Navigation" 
                        )
                        ( is-cargo 
                           "Charging" 
                           "<argument>" 
                           "Navigation" 
                        )
                     )
                  )
               )
               ( set-ets-values 12 0 0 "<argument>" ) 
               ( set-weapon-energy 0 "<argument>" ) 
               ( set-cargo 
                  "Charging" 
                  "<argument>" 
                  "Navigation" 
               )
            )
            ( when 
               ( and 
                  ( < 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( is-cargo 
                        "Charged" 
                        "<argument>" 
                        "Navigation" 
                     )
                  )
                  ( = ( mod ( mission-time ) 24 ) 0 ) 
               )
               ( set-weapon-energy 
                  ( + 
                     ( weapon-energy-pct "<argument>" ) 
                     2 
                  )
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( is-cargo 
                     "Charging" 
                     "<argument>" 
                     "Navigation" 
                  )
                  ( = ( mod ( mission-time ) 24 ) 0 ) 
               )
               ( set-cargo 
                  "Charged" 
                  "<argument>" 
                  "Navigation" 
               )
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noname" 
         )
      )
      ( when 
         ( or 
            ( and 
               ( <= ( hits-left "<argument>" ) 35 ) 
               ( > ( hits-left "<argument>" ) 0 ) 
            )
            ( = ( sim-hits-left "<argument>" ) 3 ) 
            ( destroyed-or-departed-delay 
               0 
               "<argument>" 
            )
         )
         ( set-armor-type 
            "<argument>" 
            ( true ) 
            "Heavy Armor 60" 
            "Hull" 
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "<argument>" 
         )
         ( when-argument 
            ( every-of 
               "turret03" 
               "turret04 " 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
            )
            ( true ) 
            ( turret-set-rate-of-fire 
               "@shipNameHolder[noname]" 
               50 
               "<argument>" 
            )
         )
         ( when-argument 
            ( any-of "Hull" ) 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  100 
               )
               ( > 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 5 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               2 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = 
                  ( mod 
                     ( mission-time ) 
                     ( + ( rand-multiple -3 3 ) 60 ) 
                  )
                  0 
               )
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               15 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when 
            ( not 
               ( < 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Engines" 
                  )
                  1 
               )
            )
            ( set-thrusters-status 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( = 
                  ( mod 
                     ( mission-time ) 
                     ( rand-multiple 9 11 ) 
                  )
                  0 
               )
               ( > 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Weapons" 
                  )
                  0 
               )
               ( is-in-mission "<argument>" ) 
            )
            ( weapon-create 
               "<argument>" 
               "Cruiser Flare" 
               ( get-object-x "<argument>" "Engine" ) 
               ( get-object-y "<argument>" "Engine" ) 
               ( get-object-z "<argument>" "Engine" ) 
               ( get-object-pitch "<argument>" ) 
               ( get-object-bank "<argument>" ) 
               ( get-object-heading "<argument>" ) 
            )
         )
         ( when 
            ( and 
               ( true ) 
               ( targeted "<argument>" ) 
               ( targeted "<argument>" ) 
            )
            ( hud-set-custom-gauge-active 
               ( true ) 
               "BPLowerRightMFD" 
               "BPLowerRightMFDA" 
               "BPLowerRightMFDB" 
               "BPLowerRightMFDC" 
               "BPLowerRightMFDD" 
               "BPLowerRightMFDE" 
               "BPLowerRightMFDF" 
               "BPLowerRightMFDG" 
               "BPLowerRightMFDH" 
            )
            ( hud-set-text 
               "BPLowerRightMFD" 
               "GTC Hyperion" 
            )
            ( hud-set-text 
               "BPLowerRightMFDA" 
               "Emergency Power" 
            )
            ( hud-set-text 
               "BPLowerRightMFDB" 
               "- Weapons 50%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDC" 
               "***** Armor 60%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDD" 
               "*** Repairs" 
            )
            ( hud-set-text 
               "BPLowerRightMFDE" 
               "* Maneuvering Std" 
            )
            ( hud-set-text 
               "BPLowerRightMFDF" 
               "***** Jump Cycle 2.5m" 
            )
            ( hud-set-text 
               "BPLowerRightMFDG" 
               "ECM Std" 
            )
         )
         ( when 
            ( true ) 
            ( alter-ship-flag 
               "friendly-stealth-invisible" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "free-afterburner-use" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "primaries-locked" 
               ( true ) 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( skill-level-at-least "Hard" ) 
               ( not 
                  ( are-ship-flags-set 
                     "<argument>" 
                     "secondaries-locked" 
                  )
               )
            )
            ( when-argument 
               ( every-of 
                  "Weapons" 
                  "Communication" 
                  "Communications" 
                  "Sensors" 
                  "Reactor" 
                  "Engine" 
                  "Engine01" 
                  "Engine02" 
                  "Engine03" 
                  "Engine04" 
                  "Navigation" 
                  "turret01" 
                  "turret02" 
                  "turret03" 
                  "turret04" 
                  "turret05" 
                  "turret06" 
                  "turret07" 
                  "turret08" 
                  "turret09" 
                  "turret10" 
                  "turret11" 
                  "turret12" 
                  "turret13" 
                  "turret14" 
                  "turret15" 
                  "turret16" 
                  "turret17" 
                  "turret18" 
                  "turret19" 
                  "turret20" 
                  "turret21" 
                  "turret22" 
                  "turret23" 
                  "turret24" 
                  "turret25" 
                  "turret26" 
                  "turret27" 
                  "turret28" 
                  "turret29" 
                  "turret30" 
                  "turret31" 
                  "turret32" 
                  "turret33" 
                  "turret34" 
                  "turret35" 
                  "turret36" 
                  "turret37" 
                  "turret38" 
                  "turret39" 
                  "turret40" 
                  "turret41" 
                  "turret42" 
                  "turret43" 
                  "turret44" 
                  "turret45" 
                  "turret46" 
                  "turret47" 
                  "turret48" 
                  "turret49" 
                  "turret50" 
               )
               ( true ) 
               ( set-armor-type 
                  "@shipNameHolder[noname]" 
                  ( true ) 
                  "Light Armor 60" 
                  "<argument>" 
               )
            )
         )
         ( when-argument 
            ( any-of "turret01" "turret02" ) 
            ( true ) 
            ( ship-subsys-guardian-threshold 
               15 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     16 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Shuttered" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "SHUTTERED" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     33 
                  )
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Beam Cannon" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( repair-subsystem 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
                  1 
               )
            )
         )
         ( when 
            ( true ) 
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( or 
                        ( is-cargo 
                           "Charged" 
                           "<argument>" 
                           "Navigation" 
                        )
                        ( is-cargo 
                           "Charging" 
                           "<argument>" 
                           "Navigation" 
                        )
                     )
                  )
               )
               ( set-ets-values 12 0 0 "<argument>" ) 
               ( set-weapon-energy 0 "<argument>" ) 
               ( set-cargo 
                  "Charging" 
                  "<argument>" 
                  "Navigation" 
               )
            )
            ( when 
               ( and 
                  ( < 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( is-cargo 
                        "Charged" 
                        "<argument>" 
                        "Navigation" 
                     )
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( set-weapon-energy 
                  ( + 
                     ( weapon-energy-pct "<argument>" ) 
                     2 
                  )
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( is-cargo 
                     "Charging" 
                     "<argument>" 
                     "Navigation" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( set-cargo 
                  "Charged" 
                  "<argument>" 
                  "Navigation" 
               )
            )
         )
         ( when-argument 
            ( any-of "turret65" "turret66" ) 
            ( true ) 
            ( turret-change-weapon 
               "@shipNameHolder[noname]" 
               "<argument>" 
               "Rockeye" 
               0 
               1 
            )
            ( turret-change-weapon 
               "@shipNameHolder[noname]" 
               "<argument>" 
               "Piranha#bomber" 
               0 
               2 
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noname" 
         )
      )
      ( when 
         ( or 
            ( and 
               ( destroyed-or-departed-delay 
                  0 
                  "<argument>" 
               )
               ( destroyed-or-departed-delay 
                  0 
                  "<argument>" 
               )
            )
            ( = ( sim-hits-left "<argument>" ) 99 ) 
         )
         ( do-nothing ) 
      )
      ( when 
         ( true ) 
         ( when 
            ( < 
               ( distance "Alpha 1" "<argument>" ) 
               1500 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Weapons" 
               "Weapons" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Engines" 
               "Engine" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Main Beam" 
               "turret01" 
               "turret02" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Light Pulse" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "AAA Beam" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "noName" 
            )
         )
         ( when 
            ( > 
               ( distance "Alpha 1" "<argument>" ) 
               1499 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "Weapons" 
               "Weapons" 
               "Engine" 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "noName" 
            )
         )
      )
   )
   ( when 
      ( is-ship-class 
         "GTCv Diomedes" 
         "<argument>" 
      )
      ( when 
         ( or 
            ( and 
               ( <= ( hits-left "<argument>" ) 100 ) 
               ( > ( hits-left "<argument>" ) 75 ) 
            )
            ( = ( sim-hits-left "<argument>" ) 1 ) 
         )
         ( set-armor-type 
            "<argument>" 
            ( true ) 
            "Heavy Armor 40" 
            "Hull" 
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "<argument>" 
         )
         ( when-argument 
            ( every-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret20" 
               "turret21" 
               "turret22" 
            )
            ( true ) 
            ( turret-set-rate-of-fire 
               "@shipNameHolder[noname]" 
               120 
               "<argument>" 
            )
         )
         ( when-argument 
            ( any-of "Hull" ) 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  100 
               )
               ( > 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
               ( not 
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when 
            ( not 
               ( < 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Engines" 
                  )
                  1 
               )
            )
            ( set-thrusters-status 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( > 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Weapons" 
                  )
                  0 
               )
               ( is-in-mission "<argument>" ) 
            )
            ( weapon-create 
               "<argument>" 
               "Corvette Flare" 
               ( get-object-x "<argument>" "Engine" ) 
               ( get-object-y "<argument>" "Engine" ) 
               ( get-object-z "<argument>" "Engine" ) 
               ( get-object-pitch "<argument>" ) 
               ( get-object-bank "<argument>" ) 
               ( get-object-heading "<argument>" ) 
            )
         )
         ( when 
            ( and 
               ( true ) 
               ( targeted "<argument>" ) 
               ( targeted "<argument>" ) 
            )
            ( hud-set-custom-gauge-active 
               ( true ) 
               "BPLowerRightMFD" 
               "BPLowerRightMFDA" 
               "BPLowerRightMFDB" 
               "BPLowerRightMFDC" 
               "BPLowerRightMFDD" 
               "BPLowerRightMFDE" 
               "BPLowerRightMFDF" 
               "BPLowerRightMFDG" 
               "BPLowerRightMFDH" 
            )
            ( hud-set-text 
               "BPLowerRightMFD" 
               "GTCv Diomedes" 
            )
            ( hud-set-text 
               "BPLowerRightMFDA" 
               "Reactor Rating 16" 
            )
            ( hud-set-text 
               "BPLowerRightMFDB" 
               "*** Weapons 120%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDC" 
               "***** Armor 60%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDD" 
               "** Repairs" 
            )
            ( hud-set-text 
               "BPLowerRightMFDE" 
               "* Maneuvering Std" 
            )
            ( hud-set-text 
               "BPLowerRightMFDF" 
               "***** Jump Cycle 2.5m" 
            )
            ( hud-set-text 
               "BPLowerRightMFDG" 
               "ECM Std" 
            )
         )
         ( when 
            ( true ) 
            ( alter-ship-flag 
               "friendly-stealth-invisible" 
               ( true ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "free-afterburner-use" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "primaries-locked" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( skill-level-at-least "Hard" ) 
               ( not 
                  ( are-ship-flags-set 
                     "<argument>" 
                     "secondaries-locked" 
                  )
               )
            )
            ( when-argument 
               ( every-of 
                  "Weapons" 
                  "Communication" 
                  "Communications" 
                  "Sensors" 
                  "Reactor" 
                  "Engine" 
                  "Engine01" 
                  "Engine02" 
                  "Engine03" 
                  "Engine04" 
                  "Navigation" 
                  "turret01" 
                  "turret02" 
                  "turret03" 
                  "turret04" 
                  "turret05" 
                  "turret06" 
                  "turret07" 
                  "turret08" 
                  "turret09" 
                  "turret10" 
                  "turret11" 
                  "turret12" 
                  "turret13" 
                  "turret14" 
                  "turret15" 
                  "turret16" 
                  "turret17" 
                  "turret18" 
                  "turret19" 
                  "turret20" 
                  "turret21" 
                  "turret22" 
                  "turret23" 
                  "turret24" 
                  "turret25" 
                  "turret26" 
                  "turret27" 
                  "turret28" 
                  "turret29" 
                  "turret30" 
                  "turret31" 
                  "turret32" 
                  "turret33" 
                  "turret34" 
                  "turret35" 
                  "turret36" 
                  "turret37" 
                  "turret38" 
                  "turret39" 
                  "turret40" 
                  "turret41" 
                  "turret42" 
                  "turret43" 
                  "turret44" 
                  "turret45" 
                  "turret46" 
                  "turret47" 
                  "turret48" 
                  "turret49" 
                  "turret50" 
               )
               ( true ) 
               ( set-armor-type 
                  "@shipNameHolder[noname]" 
                  ( true ) 
                  "Light Armor 60" 
                  "<argument>" 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret08" 
               "turret09" 
               "turret18" 
               "turret19" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               15 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     16 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Shuttered" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "SHUTTERED" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     33 
                  )
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Beam Cannon" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( repair-subsystem 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
                  1 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret13" 
               "turret16" 
               "turret17" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               5 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     6 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Knocked Out" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Knocked Out" 
                  "<argument>" 
               )
               ( ship-subsys-untargetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     5 
                  )
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Light Pulse" 
                  "<argument>" 
               )
               ( ship-subsys-targetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
         )
         ( when 
            ( true ) 
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( or 
                        ( is-cargo 
                           "Charged" 
                           "<argument>" 
                           "Navigation" 
                        )
                        ( is-cargo 
                           "Charging" 
                           "<argument>" 
                           "Navigation" 
                        )
                     )
                  )
               )
               ( set-ets-values 12 0 0 "<argument>" ) 
               ( set-weapon-energy 0 "<argument>" ) 
               ( set-cargo 
                  "Charging" 
                  "<argument>" 
                  "Navigation" 
               )
            )
            ( when 
               ( and 
                  ( < 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( is-cargo 
                        "Charged" 
                        "<argument>" 
                        "Navigation" 
                     )
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( set-weapon-energy 
                  ( + 
                     ( weapon-energy-pct "<argument>" ) 
                     2 
                  )
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( is-cargo 
                     "Charging" 
                     "<argument>" 
                     "Navigation" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( set-cargo 
                  "Charged" 
                  "<argument>" 
                  "Navigation" 
               )
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noname" 
         )
      )
      ( when 
         ( or 
            ( and 
               ( <= ( hits-left "<argument>" ) 75 ) 
               ( > ( hits-left "<argument>" ) 30 ) 
            )
            ( = ( sim-hits-left "<argument>" ) 2 ) 
         )
         ( set-armor-type 
            "<argument>" 
            ( true ) 
            "Heavy Armor 20" 
            "Hull" 
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "<argument>" 
         )
         ( when-argument 
            ( every-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret20" 
               "turret21" 
               "turret22" 
            )
            ( true ) 
            ( turret-set-rate-of-fire 
               "@shipNameHolder[noname]" 
               100 
               "<argument>" 
            )
         )
         ( when-argument 
            ( any-of "Hull" ) 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  100 
               )
               ( > 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 5 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               2 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = 
                  ( mod ( mission-time ) 40 ) 
                  ( rand-multiple 0 2 ) 
               )
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               25 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = 
                  ( mod ( mission-time ) 10 ) 
                  ( rand-multiple 0 2 ) 
               )
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
               ( not 
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               3 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret20" 
            )
            ( true ) 
            ( alter-ship-flag 
               "toggle-subsystem-scanning" 
               ( true ) 
               ( true ) 
               "@shipNameHolder[noname]" 
            )
            ( when 
               ( = 
                  ( mod ( mission-time ) 20 ) 
                  ( rand-multiple 0 0 ) 
               )
               ( when 
                  ( and 
                     ( or 
                        ( is-cargo 
                           "Knocked Out" 
                           "@shipNameHolder[noname]" 
                           "<argument>" 
                        )
                        ( < 
                           ( hits-left-subsystem-specific 
                              "@shipNameHolder[noname]" 
                              "<argument>" 
                           )
                           1 
                        )
                     )
                     ( are-ship-flags-set 
                        "@shipNameHolder[noname]" 
                        "toggle-subsystem-scanning" 
                     )
                  )
                  ( repair-subsystem 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                     25 
                  )
                  ( send-message 
                     "@shipNameHolder[noname]" 
                     "High" 
                     "Fixed a turret" 
                  )
                  ( alter-ship-flag 
                     "toggle-subsystem-scanning" 
                     ( false ) 
                     ( true ) 
                     "@shipNameHolder[noname]" 
                  )
               )
            )
         )
         ( when 
            ( not 
               ( < 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Engines" 
                  )
                  1 
               )
            )
            ( set-thrusters-status 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( > 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Weapons" 
                  )
                  0 
               )
               ( is-in-mission "<argument>" ) 
            )
            ( weapon-create 
               "<argument>" 
               "Corvette Flare" 
               ( get-object-x "<argument>" "Engine" ) 
               ( get-object-y "<argument>" "Engine" ) 
               ( get-object-z "<argument>" "Engine" ) 
               ( get-object-pitch "<argument>" ) 
               ( get-object-bank "<argument>" ) 
               ( get-object-heading "<argument>" ) 
            )
         )
         ( when 
            ( and 
               ( true ) 
               ( targeted "<argument>" ) 
               ( targeted "<argument>" ) 
            )
            ( hud-set-custom-gauge-active 
               ( true ) 
               "BPLowerRightMFD" 
               "BPLowerRightMFDA" 
               "BPLowerRightMFDB" 
               "BPLowerRightMFDC" 
               "BPLowerRightMFDD" 
               "BPLowerRightMFDE" 
               "BPLowerRightMFDF" 
               "BPLowerRightMFDG" 
               "BPLowerRightMFDH" 
            )
            ( hud-set-text 
               "BPLowerRightMFD" 
               "GTCv Diomedes" 
            )
            ( hud-set-text 
               "BPLowerRightMFDA" 
               "Reactor Rating 16" 
            )
            ( hud-set-text 
               "BPLowerRightMFDB" 
               "** Weapons 100%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDC" 
               "[5]*** Armor 80%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDD" 
               "***** Repairs" 
            )
            ( hud-set-text 
               "BPLowerRightMFDE" 
               "* Maneuvering Std" 
            )
            ( hud-set-text 
               "BPLowerRightMFDF" 
               "- Jump Charge" 
            )
            ( hud-set-text 
               "BPLowerRightMFDG" 
               "ECM Std" 
            )
         )
         ( when 
            ( true ) 
            ( alter-ship-flag 
               "friendly-stealth-invisible" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "free-afterburner-use" 
               ( true ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "primaries-locked" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( skill-level-at-least "Hard" ) 
               ( not 
                  ( are-ship-flags-set 
                     "<argument>" 
                     "secondaries-locked" 
                  )
               )
            )
            ( when-argument 
               ( every-of 
                  "Weapons" 
                  "Communication" 
                  "Communications" 
                  "Sensors" 
                  "Reactor" 
                  "Engine" 
                  "Engine01" 
                  "Engine02" 
                  "Engine03" 
                  "Engine04" 
                  "Navigation" 
                  "turret01" 
                  "turret02" 
                  "turret03" 
                  "turret04" 
                  "turret05" 
                  "turret06" 
                  "turret07" 
                  "turret08" 
                  "turret09" 
                  "turret10" 
                  "turret11" 
                  "turret12" 
                  "turret13" 
                  "turret14" 
                  "turret15" 
                  "turret16" 
                  "turret17" 
                  "turret18" 
                  "turret19" 
                  "turret20" 
                  "turret21" 
                  "turret22" 
                  "turret23" 
                  "turret24" 
                  "turret25" 
                  "turret26" 
                  "turret27" 
                  "turret28" 
                  "turret29" 
                  "turret30" 
                  "turret31" 
                  "turret32" 
                  "turret33" 
                  "turret34" 
                  "turret35" 
                  "turret36" 
                  "turret37" 
                  "turret38" 
                  "turret39" 
                  "turret40" 
                  "turret41" 
                  "turret42" 
                  "turret43" 
                  "turret44" 
                  "turret45" 
                  "turret46" 
                  "turret47" 
                  "turret48" 
                  "turret49" 
                  "turret50" 
               )
               ( true ) 
               ( set-armor-type 
                  "@shipNameHolder[noname]" 
                  ( true ) 
                  "Light Armor 40" 
                  "<argument>" 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret08" 
               "turret09" 
               "turret18" 
               "turret19" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               15 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     16 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Shuttered" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "SHUTTERED" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     33 
                  )
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Beam Cannon" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( repair-subsystem 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
                  1 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret16" 
               "turret17" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               5 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     6 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Knocked Out" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Knocked Out" 
                  "<argument>" 
               )
               ( ship-subsys-untargetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     5 
                  )
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Light Pulse" 
                  "<argument>" 
               )
               ( ship-subsys-targetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
         )
         ( when 
            ( true ) 
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( or 
                        ( is-cargo 
                           "Charged" 
                           "<argument>" 
                           "Navigation" 
                        )
                        ( is-cargo 
                           "Charging" 
                           "<argument>" 
                           "Navigation" 
                        )
                     )
                  )
               )
               ( set-ets-values 12 0 0 "<argument>" ) 
               ( set-weapon-energy 0 "<argument>" ) 
               ( set-cargo 
                  "Charging" 
                  "<argument>" 
                  "Navigation" 
               )
            )
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( is-cargo 
                     "Charging" 
                     "<argument>" 
                     "Navigation" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( set-cargo 
                  "Charged" 
                  "<argument>" 
                  "Navigation" 
               )
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noname" 
         )
      )
      ( when 
         ( or 
            ( and 
               ( <= ( hits-left "<argument>" ) 30 ) 
               ( > ( hits-left "<argument>" ) 0 ) 
            )
            ( = ( sim-hits-left "<argument>" ) 3 ) 
            ( destroyed-or-departed-delay 
               0 
               "<argument>" 
            )
         )
         ( set-armor-type 
            "<argument>" 
            ( true ) 
            "Heavy Armor 80" 
            "Hull" 
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "<argument>" 
         )
         ( when-argument 
            ( every-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret20" 
               "turret21" 
               "turret22" 
            )
            ( true ) 
            ( turret-set-rate-of-fire 
               "@shipNameHolder[noname]" 
               80 
               "<argument>" 
            )
         )
         ( when-argument 
            ( any-of "Hull" ) 
            ( and 
               ( = ( mod ( mission-time ) 20 ) 0 ) 
               ( < 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  100 
               )
               ( > 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 5 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = 
                  ( mod ( mission-time ) 60 ) 
                  ( rand-multiple 0 2 ) 
               )
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               15 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
               ( not 
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when 
            ( not 
               ( < 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Engines" 
                  )
                  1 
               )
            )
            ( set-thrusters-status 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( = 
                  ( mod ( mission-time ) 10 ) 
                  ( rand-multiple 0 2 ) 
               )
               ( > 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Weapons" 
                  )
                  0 
               )
               ( is-in-mission "<argument>" ) 
            )
            ( weapon-create 
               "<argument>" 
               "Corvette Flare" 
               ( get-object-x "<argument>" "Engine" ) 
               ( get-object-y "<argument>" "Engine" ) 
               ( get-object-z "<argument>" "Engine" ) 
               ( get-object-pitch "<argument>" ) 
               ( get-object-bank "<argument>" ) 
               ( get-object-heading "<argument>" ) 
            )
         )
         ( when 
            ( and 
               ( true ) 
               ( targeted "<argument>" ) 
               ( targeted "<argument>" ) 
            )
            ( hud-set-custom-gauge-active 
               ( true ) 
               "BPLowerRightMFD" 
               "BPLowerRightMFDA" 
               "BPLowerRightMFDB" 
               "BPLowerRightMFDC" 
               "BPLowerRightMFDD" 
               "BPLowerRightMFDE" 
               "BPLowerRightMFDF" 
               "BPLowerRightMFDG" 
               "BPLowerRightMFDH" 
            )
            ( hud-set-text 
               "BPLowerRightMFD" 
               "GTCv Diomedes" 
            )
            ( hud-set-text 
               "BPLowerRightMFDA" 
               "Emergency Power" 
            )
            ( hud-set-text 
               "BPLowerRightMFDB" 
               "* Weapons 80%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDC" 
               "[5]*** Armor 80%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDD" 
               "*** Repairs" 
            )
            ( hud-set-text 
               "BPLowerRightMFDE" 
               "* Maneuvering Std" 
            )
            ( hud-set-text 
               "BPLowerRightMFDF" 
               "***** Jump Cycle 2.5m" 
            )
            ( hud-set-text 
               "BPLowerRightMFDG" 
               "ECM Std" 
            )
         )
         ( when 
            ( true ) 
            ( alter-ship-flag 
               "friendly-stealth-invisible" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "free-afterburner-use" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "primaries-locked" 
               ( true ) 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( skill-level-at-least "Hard" ) 
               ( not 
                  ( are-ship-flags-set 
                     "<argument>" 
                     "secondaries-locked" 
                  )
               )
            )
            ( when-argument 
               ( every-of 
                  "Weapons" 
                  "Communication" 
                  "Communications" 
                  "Sensors" 
                  "Reactor" 
                  "Engine" 
                  "Engine01" 
                  "Engine02" 
                  "Engine03" 
                  "Engine04" 
                  "Navigation" 
                  "turret01" 
                  "turret02" 
                  "turret03" 
                  "turret04" 
                  "turret05" 
                  "turret06" 
                  "turret07" 
                  "turret08" 
                  "turret09" 
                  "turret10" 
                  "turret11" 
                  "turret12" 
                  "turret13" 
                  "turret14" 
                  "turret15" 
                  "turret16" 
                  "turret17" 
                  "turret18" 
                  "turret19" 
                  "turret20" 
                  "turret21" 
                  "turret22" 
                  "turret23" 
                  "turret24" 
                  "turret25" 
                  "turret26" 
                  "turret27" 
                  "turret28" 
                  "turret29" 
                  "turret30" 
                  "turret31" 
                  "turret32" 
                  "turret33" 
                  "turret34" 
                  "turret35" 
                  "turret36" 
                  "turret37" 
                  "turret38" 
                  "turret39" 
                  "turret40" 
                  "turret41" 
                  "turret42" 
                  "turret43" 
                  "turret44" 
                  "turret45" 
                  "turret46" 
                  "turret47" 
                  "turret48" 
                  "turret49" 
                  "turret50" 
               )
               ( true ) 
               ( set-armor-type 
                  "@shipNameHolder[noname]" 
                  ( true ) 
                  "Light Armor 60" 
                  "<argument>" 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret08" 
               "turret09" 
               "turret18" 
               "turret19" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               15 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     16 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Shuttered" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "SHUTTERED" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     33 
                  )
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Beam Cannon" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( repair-subsystem 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
                  1 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret13" 
               "turret16" 
               "turret17" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               5 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     6 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Knocked Out" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Knocked Out" 
                  "<argument>" 
               )
               ( ship-subsys-untargetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     5 
                  )
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Light Pulse" 
                  "<argument>" 
               )
               ( ship-subsys-targetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
         )
         ( when 
            ( true ) 
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( or 
                        ( is-cargo 
                           "Charged" 
                           "<argument>" 
                           "Navigation" 
                        )
                        ( is-cargo 
                           "Charging" 
                           "<argument>" 
                           "Navigation" 
                        )
                     )
                  )
               )
               ( set-ets-values 12 0 0 "<argument>" ) 
               ( set-weapon-energy 0 "<argument>" ) 
               ( set-cargo 
                  "Charging" 
                  "<argument>" 
                  "Navigation" 
               )
            )
            ( when 
               ( and 
                  ( < 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( is-cargo 
                        "Charged" 
                        "<argument>" 
                        "Navigation" 
                     )
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( set-weapon-energy 
                  ( + 
                     ( weapon-energy-pct "<argument>" ) 
                     2 
                  )
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( is-cargo 
                     "Charging" 
                     "<argument>" 
                     "Navigation" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( set-cargo 
                  "Charged" 
                  "<argument>" 
                  "Navigation" 
               )
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noname" 
         )
      )
      ( when 
         ( or 
            ( and 
               ( destroyed-or-departed-delay 
                  0 
                  "<argument>" 
               )
               ( destroyed-or-departed-delay 
                  0 
                  "<argument>" 
               )
            )
            ( = ( sim-hits-left "<argument>" ) 99 ) 
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noname" 
         )
      )
      ( when 
         ( missile-locked 0 ) 
         ( do-nothing ) 
      )
      ( when 
         ( true ) 
         ( when 
            ( < 
               ( distance "Alpha 1" "<argument>" ) 
               1500 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Weapons" 
               "Weapons" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Engines" 
               "Engine" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Main Beam" 
               "turret08" 
               "turret09" 
               "turret18" 
               "turret19" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Light Pulse" 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret16" 
               "turret17" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "AAA Beam" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret20" 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "noName" 
            )
         )
         ( when 
            ( > 
               ( distance "Alpha 1" "<argument>" ) 
               1499 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "Weapons" 
               "Weapons" 
               "Engine" 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "noName" 
            )
         )
      )
   )
   ( when 
      ( is-ship-class 
         "GTD Erebus" 
         "<argument>" 
      )
      ( when 
         ( or 
            ( and 
               ( <= ( hits-left "<argument>" ) 100 ) 
               ( > ( hits-left "<argument>" ) 70 ) 
            )
            ( = ( sim-hits-left "<argument>" ) 1 ) 
         )
         ( set-armor-type 
            "<argument>" 
            ( true ) 
            "Heavy Armor 20" 
            "Hull" 
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "<argument>" 
         )
         ( when-argument 
            ( every-of 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
               "turret51" 
               "turret52" 
               "turret53" 
               "turret54" 
               "turret55" 
               "turret56" 
               "turret57" 
               "turret58" 
               "turret59" 
               "turret60" 
               "turret61" 
               "turret62" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( true ) 
            ( turret-set-rate-of-fire 
               "@shipNameHolder[noname]" 
               200 
               "<argument>" 
            )
         )
         ( when-argument 
            ( any-of "Hull" ) 
            ( and 
               ( = ( mod ( mission-time ) 20 ) 0 ) 
               ( < 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  100 
               )
               ( > 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               2 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 60 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               15 
            )
         )
         ( when-argument 
            ( any-of 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
               "turret51" 
               "turret52" 
               "turret53" 
               "turret54" 
               "turret55" 
               "turret56" 
               "turret57" 
               "turret58" 
               "turret59" 
               "turret60" 
               "turret61" 
               "turret62" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
               ( not 
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
               "turret51" 
               "turret52" 
               "turret53" 
               "turret54" 
               "turret55" 
               "turret56" 
               "turret57" 
               "turret58" 
               "turret59" 
               "turret60" 
               "turret61" 
               "turret62" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               0 
            )
         )
         ( when 
            ( not 
               ( < 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Engines" 
                  )
                  1 
               )
            )
            ( set-thrusters-status 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( > 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Weapons" 
                  )
                  0 
               )
               ( is-in-mission "<argument>" ) 
            )
            ( weapon-create 
               "<argument>" 
               "Corvette Flare" 
               ( get-object-x "<argument>" "Engine" ) 
               ( get-object-y "<argument>" "Engine" ) 
               ( get-object-z "<argument>" "Engine" ) 
               ( get-object-pitch "<argument>" ) 
               ( get-object-bank "<argument>" ) 
               ( get-object-heading "<argument>" ) 
            )
         )
         ( when 
            ( and 
               ( true ) 
               ( targeted "<argument>" ) 
               ( targeted "<argument>" ) 
            )
            ( hud-set-custom-gauge-active 
               ( true ) 
               "BPLowerRightMFD" 
               "BPLowerRightMFDA" 
               "BPLowerRightMFDB" 
               "BPLowerRightMFDC" 
               "BPLowerRightMFDD" 
               "BPLowerRightMFDE" 
               "BPLowerRightMFDF" 
               "BPLowerRightMFDG" 
               "BPLowerRightMFDH" 
            )
            ( hud-set-text 
               "BPLowerRightMFD" 
               "GTD Erebus" 
            )
            ( hud-set-text 
               "BPLowerRightMFDA" 
               "Reactor Rating 36" 
            )
            ( hud-set-text 
               "BPLowerRightMFDB" 
               "[10]*** Weapons 200%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDC" 
               "[8]*** Armor 80%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDD" 
               "*** Repairs" 
            )
            ( hud-set-text 
               "BPLowerRightMFDE" 
               "*** Maneuvering" 
            )
            ( hud-set-text 
               "BPLowerRightMFDF" 
               "[5]*** Jump Cycle 2m" 
            )
            ( hud-set-text 
               "BPLowerRightMFDG" 
               "ECM Enhanced" 
            )
         )
         ( when 
            ( true ) 
            ( alter-ship-flag 
               "friendly-stealth-invisible" 
               ( true ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "free-afterburner-use" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "primaries-locked" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( skill-level-at-least "Hard" ) 
               ( not 
                  ( are-ship-flags-set 
                     "<argument>" 
                     "secondaries-locked" 
                  )
               )
            )
            ( when-argument 
               ( every-of 
                  "Weapons" 
                  "Communication" 
                  "Communications" 
                  "Sensors" 
                  "Reactor" 
                  "Engine" 
                  "Engine01" 
                  "Engine02" 
                  "Engine03" 
                  "Engine04" 
                  "Navigation" 
                  "turret01" 
                  "turret02" 
                  "turret03" 
                  "turret04" 
                  "turret05" 
                  "turret06" 
                  "turret07" 
                  "turret08" 
                  "turret09" 
                  "turret10" 
                  "turret11" 
                  "turret12" 
                  "turret13" 
                  "turret14" 
                  "turret15" 
                  "turret16" 
                  "turret17" 
                  "turret18" 
                  "turret19" 
                  "turret20" 
                  "turret21" 
                  "turret22" 
                  "turret23" 
                  "turret24" 
                  "turret25" 
                  "turret26" 
                  "turret27" 
                  "turret28" 
                  "turret29" 
                  "turret30" 
                  "turret31" 
                  "turret32" 
                  "turret33" 
                  "turret34" 
                  "turret35" 
                  "turret36" 
                  "turret37" 
                  "turret38" 
                  "turret39" 
                  "turret40" 
                  "turret41" 
                  "turret42" 
                  "turret43" 
                  "turret44" 
                  "turret45" 
                  "turret46" 
                  "turret47" 
                  "turret48" 
                  "turret49" 
                  "turret50" 
                  "turret51" 
                  "turret52" 
                  "turret53" 
                  "turret54" 
                  "turret55" 
                  "turret56" 
                  "turret57" 
                  "turret58" 
                  "turret59" 
                  "turret60" 
                  "turret61" 
                  "turret62" 
                  "turret63" 
                  "turret64" 
                  "turret65" 
                  "turret66" 
               )
               ( true ) 
               ( set-armor-type 
                  "@shipNameHolder[noname]" 
                  ( true ) 
                  "Light Armor 40" 
                  "<argument>" 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               15 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     16 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Shuttered" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "SHUTTERED" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     33 
                  )
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Beam Cannon" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( repair-subsystem 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
                  1 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret13" 
               "turret16" 
               "turret17" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               5 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     6 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Knocked Out" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Knocked Out" 
                  "<argument>" 
               )
               ( ship-subsys-untargetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     5 
                  )
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Light Pulse" 
                  "<argument>" 
               )
               ( ship-subsys-targetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
         )
         ( when 
            ( true ) 
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( or 
                        ( is-cargo 
                           "Charged" 
                           "<argument>" 
                           "Navigation" 
                        )
                        ( is-cargo 
                           "Charging" 
                           "<argument>" 
                           "Navigation" 
                        )
                     )
                  )
               )
               ( set-ets-values 12 0 0 "<argument>" ) 
               ( set-weapon-energy 0 "<argument>" ) 
               ( set-cargo 
                  "Charging" 
                  "<argument>" 
                  "Navigation" 
               )
            )
            ( when 
               ( and 
                  ( < 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( is-cargo 
                        "Charged" 
                        "<argument>" 
                        "Navigation" 
                     )
                  )
                  ( = ( mod ( mission-time ) 2 ) 0 ) 
               )
               ( set-weapon-energy 
                  ( + 
                     ( weapon-energy-pct "<argument>" ) 
                     2 
                  )
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( is-cargo 
                     "Charging" 
                     "<argument>" 
                     "Navigation" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( set-cargo 
                  "Charged" 
                  "<argument>" 
                  "Navigation" 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
            )
            ( true ) 
            ( turret-set-target-priorities 
               "@shipNameHolder[noname]" 
               "<argument>" 
               ( true ) 
               "bombers" 
               "cruisers" 
               "corvettes" 
               "capitals" 
               "super caps" 
               "fighters" 
               "bombs" 
               "asteroids" 
            )
         )
         ( when-argument 
            ( any-of 
               "turret65" 
               "turret66" 
               "turret63" 
               "turret64" 
            )
            ( true ) 
            ( turret-change-weapon 
               "@shipNameHolder[noname]" 
               "<argument>" 
               "Angel Flare" 
               0 
               1 
            )
            ( turret-change-weapon 
               "@shipNameHolder[noname]" 
               "<argument>" 
               "Piranha#bomber" 
               0 
               2 
            )
            ( turret-change-weapon 
               "@shipNameHolder[noname]" 
               "<argument>" 
               "Rockeye" 
               0 
               3 
            )
            ( turret-change-weapon 
               "@shipNameHolder[noname]" 
               "<argument>" 
               "Trebuchet#aegis" 
               0 
               4 
            )
            ( turret-set-target-priorities 
               "@shipNameHolder[noname]" 
               "<argument>" 
               ( true ) 
               "bombs" 
               "bombers" 
               "ships" 
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noname" 
         )
      )
      ( when 
         ( or 
            ( and 
               ( <= ( hits-left "<argument>" ) 70 ) 
               ( > ( hits-left "<argument>" ) 20 ) 
            )
            ( = ( sim-hits-left "<argument>" ) 2 ) 
         )
         ( set-armor-type 
            "<argument>" 
            ( true ) 
            "Heavy Armor 5" 
            "Hull" 
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "<argument>" 
         )
         ( when-argument 
            ( every-of 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
               "turret51" 
               "turret52" 
               "turret53" 
               "turret54" 
               "turret55" 
               "turret56" 
               "turret57" 
               "turret58" 
               "turret59" 
               "turret60" 
               "turret61" 
               "turret62" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( true ) 
            ( turret-set-rate-of-fire 
               "@shipNameHolder[noname]" 
               200 
               "<argument>" 
            )
         )
         ( when-argument 
            ( any-of "Hull" ) 
            ( and 
               ( = ( mod ( mission-time ) 20 ) 0 ) 
               ( < 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  100 
               )
               ( > 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               6 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 20 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               35 
            )
         )
         ( when-argument 
            ( any-of 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
               "turret51" 
               "turret52" 
               "turret53" 
               "turret54" 
               "turret55" 
               "turret56" 
               "turret57" 
               "turret58" 
               "turret59" 
               "turret60" 
               "turret61" 
               "turret62" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
               ( not 
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               5 
            )
         )
         ( when-argument 
            ( any-of 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
               "turret51" 
               "turret52" 
               "turret53" 
               "turret54" 
               "turret55" 
               "turret56" 
               "turret57" 
               "turret58" 
               "turret59" 
               "turret60" 
               "turret61" 
               "turret62" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( true ) 
            ( alter-ship-flag 
               "toggle-subsystem-scanning" 
               ( true ) 
               ( true ) 
               "@shipNameHolder[noname]" 
            )
            ( when 
               ( = 
                  ( mod ( mission-time ) 20 ) 
                  ( rand-multiple 0 0 ) 
               )
               ( when 
                  ( and 
                     ( or 
                        ( is-cargo 
                           "Knocked Out" 
                           "@shipNameHolder[noname]" 
                           "<argument>" 
                        )
                        ( < 
                           ( hits-left-subsystem-specific 
                              "@shipNameHolder[noname]" 
                              "<argument>" 
                           )
                           1 
                        )
                     )
                     ( are-ship-flags-set 
                        "@shipNameHolder[noname]" 
                        "toggle-subsystem-scanning" 
                     )
                  )
                  ( repair-subsystem 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                     25 
                  )
                  ( send-message 
                     "@shipNameHolder[noname]" 
                     "High" 
                     "Fixed a turret" 
                  )
                  ( alter-ship-flag 
                     "toggle-subsystem-scanning" 
                     ( false ) 
                     ( true ) 
                     "@shipNameHolder[noname]" 
                  )
               )
            )
         )
         ( when 
            ( not 
               ( < 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Engines" 
                  )
                  1 
               )
            )
            ( set-thrusters-status 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( > 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Weapons" 
                  )
                  0 
               )
               ( is-in-mission "<argument>" ) 
            )
            ( weapon-create 
               "<argument>" 
               "Corvette Flare" 
               ( get-object-x "<argument>" "Engine" ) 
               ( get-object-y "<argument>" "Engine" ) 
               ( get-object-z "<argument>" "Engine" ) 
               ( get-object-pitch "<argument>" ) 
               ( get-object-bank "<argument>" ) 
               ( get-object-heading "<argument>" ) 
            )
         )
         ( when 
            ( and 
               ( true ) 
               ( targeted "<argument>" ) 
               ( targeted "<argument>" ) 
            )
            ( hud-set-custom-gauge-active 
               ( true ) 
               "BPLowerRightMFD" 
               "BPLowerRightMFDA" 
               "BPLowerRightMFDB" 
               "BPLowerRightMFDC" 
               "BPLowerRightMFDD" 
               "BPLowerRightMFDE" 
               "BPLowerRightMFDF" 
               "BPLowerRightMFDG" 
               "BPLowerRightMFDH" 
            )
            ( hud-set-text 
               "BPLowerRightMFD" 
               "GTD Erebus" 
            )
            ( hud-set-text 
               "BPLowerRightMFDA" 
               "Reactor Rating 36" 
            )
            ( hud-set-text 
               "BPLowerRightMFDB" 
               "[10]*** Weapons 200%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDC" 
               "[10]*** Armor 95%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDD" 
               "[5]*** Repairs" 
            )
            ( hud-set-text 
               "BPLowerRightMFDE" 
               "[5] Maneuvering" 
            )
            ( hud-set-text 
               "BPLowerRightMFDF" 
               "- No Jump Charge" 
            )
            ( hud-set-text 
               "BPLowerRightMFDG" 
               "ECM Standard" 
            )
         )
         ( when 
            ( true ) 
            ( alter-ship-flag 
               "friendly-stealth-invisible" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "free-afterburner-use" 
               ( true ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "primaries-locked" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( skill-level-at-least "Hard" ) 
               ( not 
                  ( are-ship-flags-set 
                     "<argument>" 
                     "secondaries-locked" 
                  )
               )
            )
            ( when-argument 
               ( every-of 
                  "Weapons" 
                  "Communication" 
                  "Communications" 
                  "Sensors" 
                  "Reactor" 
                  "Engine" 
                  "Engine01" 
                  "Engine02" 
                  "Engine03" 
                  "Engine04" 
                  "Navigation" 
                  "turret01" 
                  "turret02" 
                  "turret03" 
                  "turret04" 
                  "turret05" 
                  "turret06" 
                  "turret07" 
                  "turret08" 
                  "turret09" 
                  "turret10" 
                  "turret11" 
                  "turret12" 
                  "turret13" 
                  "turret14" 
                  "turret15" 
                  "turret16" 
                  "turret17" 
                  "turret18" 
                  "turret19" 
                  "turret20" 
                  "turret21" 
                  "turret22" 
                  "turret23" 
                  "turret24" 
                  "turret25" 
                  "turret26" 
                  "turret27" 
                  "turret28" 
                  "turret29" 
                  "turret30" 
                  "turret31" 
                  "turret32" 
                  "turret33" 
                  "turret34" 
                  "turret35" 
                  "turret36" 
                  "turret37" 
                  "turret38" 
                  "turret39" 
                  "turret40" 
                  "turret41" 
                  "turret42" 
                  "turret43" 
                  "turret44" 
                  "turret45" 
                  "turret46" 
                  "turret47" 
                  "turret48" 
                  "turret49" 
                  "turret50" 
                  "turret51" 
                  "turret52" 
                  "turret53" 
                  "turret54" 
                  "turret55" 
                  "turret56" 
                  "turret57" 
                  "turret58" 
                  "turret59" 
                  "turret60" 
                  "turret61" 
                  "turret62" 
                  "turret63" 
                  "turret64" 
                  "turret65" 
                  "turret66" 
               )
               ( true ) 
               ( set-armor-type 
                  "@shipNameHolder[noname]" 
                  ( true ) 
                  "Light Armor 20" 
                  "<argument>" 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               15 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     16 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Shuttered" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "SHUTTERED" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     33 
                  )
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Beam Cannon" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( repair-subsystem 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
                  1 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret13" 
               "turret16" 
               "turret17" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               5 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     6 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Knocked Out" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Knocked Out" 
                  "<argument>" 
               )
               ( ship-subsys-untargetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     5 
                  )
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Light Pulse" 
                  "<argument>" 
               )
               ( ship-subsys-targetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
         )
         ( when 
            ( true ) 
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( or 
                        ( is-cargo 
                           "Charged" 
                           "<argument>" 
                           "Navigation" 
                        )
                        ( is-cargo 
                           "Charging" 
                           "<argument>" 
                           "Navigation" 
                        )
                     )
                  )
               )
               ( set-ets-values 12 0 0 "<argument>" ) 
               ( set-weapon-energy 0 "<argument>" ) 
               ( set-cargo 
                  "Charging" 
                  "<argument>" 
                  "Navigation" 
               )
            )
            ( when 
               ( and 
                  ( < 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( is-cargo 
                        "Charged" 
                        "<argument>" 
                        "Navigation" 
                     )
                  )
                  ( = ( mod ( mission-time ) 2 ) 0 ) 
               )
               ( set-weapon-energy 
                  ( + 
                     ( weapon-energy-pct "<argument>" ) 
                     0 
                  )
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( is-cargo 
                     "Charging" 
                     "<argument>" 
                     "Navigation" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( set-cargo 
                  "Charged" 
                  "<argument>" 
                  "Navigation" 
               )
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noname" 
         )
      )
      ( when 
         ( or 
            ( and 
               ( <= ( hits-left "<argument>" ) 20 ) 
               ( > ( hits-left "<argument>" ) 0 ) 
            )
            ( = ( sim-hits-left "<argument>" ) 3 ) 
         )
         ( set-armor-type 
            "<argument>" 
            ( true ) 
            "Heavy Armor 5" 
            "Hull" 
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "<argument>" 
         )
         ( when-argument 
            ( every-of 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
               "turret51" 
               "turret52" 
               "turret53" 
               "turret54" 
               "turret55" 
               "turret56" 
               "turret57" 
               "turret58" 
               "turret59" 
               "turret60" 
               "turret61" 
               "turret62" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( true ) 
            ( turret-set-rate-of-fire 
               "@shipNameHolder[noname]" 
               50 
               "<argument>" 
            )
         )
         ( when-argument 
            ( any-of "Hull" ) 
            ( and 
               ( = ( mod ( mission-time ) 20 ) 0 ) 
               ( < 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  100 
               )
               ( > 
                  ( hits-left "@shipNameHolder[noname]" ) 
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               1 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               6 
            )
         )
         ( when-argument 
            ( any-of 
               "Communication" 
               "Sensors" 
               "Weapons" 
               "Navigation" 
               "Engines" 
               "Engine" 
               "Engine01" 
               "Engine02" 
               "Engine03" 
               "Engine04" 
               "Reactor" 
            )
            ( and 
               ( = ( mod ( mission-time ) 20 ) 0 ) 
               ( = 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               35 
            )
         )
         ( when-argument 
            ( any-of 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
               "turret51" 
               "turret52" 
               "turret53" 
               "turret54" 
               "turret55" 
               "turret56" 
               "turret57" 
               "turret58" 
               "turret59" 
               "turret60" 
               "turret61" 
               "turret62" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( < 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  100 
               )
               ( > 
                  ( hits-left-subsystem-specific 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  0 
               )
               ( not 
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
            )
            ( repair-subsystem 
               "@shipNameHolder[noname]" 
               "<argument>" 
               5 
            )
         )
         ( when-argument 
            ( any-of 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret37" 
               "turret38" 
               "turret39" 
               "turret40" 
               "turret41" 
               "turret42" 
               "turret43" 
               "turret44" 
               "turret45" 
               "turret46" 
               "turret47" 
               "turret48" 
               "turret49" 
               "turret50" 
               "turret51" 
               "turret52" 
               "turret53" 
               "turret54" 
               "turret55" 
               "turret56" 
               "turret57" 
               "turret58" 
               "turret59" 
               "turret60" 
               "turret61" 
               "turret62" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( true ) 
            ( alter-ship-flag 
               "toggle-subsystem-scanning" 
               ( true ) 
               ( true ) 
               "@shipNameHolder[noname]" 
            )
            ( when 
               ( = 
                  ( mod ( mission-time ) 20 ) 
                  ( rand-multiple 0 0 ) 
               )
               ( when 
                  ( and 
                     ( or 
                        ( is-cargo 
                           "Knocked Out" 
                           "@shipNameHolder[noname]" 
                           "<argument>" 
                        )
                        ( < 
                           ( hits-left-subsystem-specific 
                              "@shipNameHolder[noname]" 
                              "<argument>" 
                           )
                           1 
                        )
                     )
                     ( are-ship-flags-set 
                        "@shipNameHolder[noname]" 
                        "toggle-subsystem-scanning" 
                     )
                  )
                  ( repair-subsystem 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                     25 
                  )
                  ( send-message 
                     "@shipNameHolder[noname]" 
                     "High" 
                     "Fixed a turret" 
                  )
                  ( alter-ship-flag 
                     "toggle-subsystem-scanning" 
                     ( false ) 
                     ( true ) 
                     "@shipNameHolder[noname]" 
                  )
               )
            )
         )
         ( when 
            ( not 
               ( < 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Engines" 
                  )
                  1 
               )
            )
            ( set-thrusters-status 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( = ( mod ( mission-time ) 10 ) 0 ) 
               ( > 
                  ( hits-left-subsystem-generic 
                     "<argument>" 
                     "Weapons" 
                  )
                  0 
               )
               ( is-in-mission "<argument>" ) 
            )
            ( weapon-create 
               "<argument>" 
               "Corvette Flare" 
               ( get-object-x "<argument>" "Engine" ) 
               ( get-object-y "<argument>" "Engine" ) 
               ( get-object-z "<argument>" "Engine" ) 
               ( get-object-pitch "<argument>" ) 
               ( get-object-bank "<argument>" ) 
               ( get-object-heading "<argument>" ) 
            )
         )
         ( when 
            ( and 
               ( true ) 
               ( targeted "<argument>" ) 
               ( targeted "<argument>" ) 
            )
            ( hud-set-custom-gauge-active 
               ( true ) 
               "BPLowerRightMFD" 
               "BPLowerRightMFDA" 
               "BPLowerRightMFDB" 
               "BPLowerRightMFDC" 
               "BPLowerRightMFDD" 
               "BPLowerRightMFDE" 
               "BPLowerRightMFDF" 
               "BPLowerRightMFDG" 
               "BPLowerRightMFDH" 
            )
            ( hud-set-text 
               "BPLowerRightMFD" 
               "GTD Erebus" 
            )
            ( hud-set-text 
               "BPLowerRightMFDA" 
               "EMERGENCY POWER" 
            )
            ( hud-set-text 
               "BPLowerRightMFDB" 
               "* Weapons 50%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDC" 
               "[10]*** Armor 95%" 
            )
            ( hud-set-text 
               "BPLowerRightMFDD" 
               "[5]*** Repairs" 
            )
            ( hud-set-text 
               "BPLowerRightMFDE" 
               "[5] Maneuvering" 
            )
            ( hud-set-text 
               "BPLowerRightMFDF" 
               "[10]*** Jump Cycle 1m" 
            )
            ( hud-set-text 
               "BPLowerRightMFDG" 
               "ECM Standard" 
            )
         )
         ( when 
            ( true ) 
            ( alter-ship-flag 
               "friendly-stealth-invisible" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "free-afterburner-use" 
               ( false ) 
               ( true ) 
               "<argument>" 
            )
            ( alter-ship-flag 
               "primaries-locked" 
               ( true ) 
               ( true ) 
               "<argument>" 
            )
         )
         ( when 
            ( and 
               ( skill-level-at-least "Hard" ) 
               ( not 
                  ( are-ship-flags-set 
                     "<argument>" 
                     "secondaries-locked" 
                  )
               )
            )
            ( when-argument 
               ( every-of 
                  "Weapons" 
                  "Communication" 
                  "Communications" 
                  "Sensors" 
                  "Reactor" 
                  "Engine" 
                  "Engine01" 
                  "Engine02" 
                  "Engine03" 
                  "Engine04" 
                  "Navigation" 
                  "turret01" 
                  "turret02" 
                  "turret03" 
                  "turret04" 
                  "turret05" 
                  "turret06" 
                  "turret07" 
                  "turret08" 
                  "turret09" 
                  "turret10" 
                  "turret11" 
                  "turret12" 
                  "turret13" 
                  "turret14" 
                  "turret15" 
                  "turret16" 
                  "turret17" 
                  "turret18" 
                  "turret19" 
                  "turret20" 
                  "turret21" 
                  "turret22" 
                  "turret23" 
                  "turret24" 
                  "turret25" 
                  "turret26" 
                  "turret27" 
                  "turret28" 
                  "turret29" 
                  "turret30" 
                  "turret31" 
                  "turret32" 
                  "turret33" 
                  "turret34" 
                  "turret35" 
                  "turret36" 
                  "turret37" 
                  "turret38" 
                  "turret39" 
                  "turret40" 
                  "turret41" 
                  "turret42" 
                  "turret43" 
                  "turret44" 
                  "turret45" 
                  "turret46" 
                  "turret47" 
                  "turret48" 
                  "turret49" 
                  "turret50" 
                  "turret51" 
                  "turret52" 
                  "turret53" 
                  "turret54" 
                  "turret55" 
                  "turret56" 
                  "turret57" 
                  "turret58" 
                  "turret59" 
                  "turret60" 
                  "turret61" 
                  "turret62" 
                  "turret63" 
                  "turret64" 
                  "turret65" 
                  "turret66" 
               )
               ( true ) 
               ( set-armor-type 
                  "@shipNameHolder[noname]" 
                  ( true ) 
                  "Light Armor 20" 
                  "<argument>" 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               15 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     16 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Shuttered" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "SHUTTERED" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     33 
                  )
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Beam Cannon" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( is-cargo 
                     "Shuttered" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( repair-subsystem 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
                  1 
               )
            )
         )
         ( when-argument 
            ( any-of 
               "turret01" 
               "turret02" 
               "turret13" 
               "turret16" 
               "turret17" 
            )
            ( true ) 
            ( ship-subsys-guardian-threshold 
               5 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( when 
               ( and 
                  ( < 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     6 
                  )
                  ( is-cargo 
                     "Nothing" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-lock 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Knocked Out" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Knocked Out" 
                  "<argument>" 
               )
               ( ship-subsys-untargetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( > 
                     ( hits-left-subsystem-specific 
                        "@shipNameHolder[noname]" 
                        "<argument>" 
                     )
                     5 
                  )
                  ( is-cargo 
                     "Knocked Out" 
                     "@shipNameHolder[noname]" 
                     "<argument>" 
                  )
               )
               ( turret-free 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( set-cargo 
                  "Nothing" 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
               ( change-subsystem-name 
                  "@shipNameHolder[noname]" 
                  "Light Pulse" 
                  "<argument>" 
               )
               ( ship-subsys-targetable 
                  "@shipNameHolder[noname]" 
                  "<argument>" 
               )
            )
         )
         ( when 
            ( true ) 
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( or 
                        ( is-cargo 
                           "Charged" 
                           "<argument>" 
                           "Navigation" 
                        )
                        ( is-cargo 
                           "Charging" 
                           "<argument>" 
                           "Navigation" 
                        )
                     )
                  )
               )
               ( set-ets-values 12 0 0 "<argument>" ) 
               ( set-weapon-energy 0 "<argument>" ) 
               ( set-cargo 
                  "Charging" 
                  "<argument>" 
                  "Navigation" 
               )
            )
            ( when 
               ( and 
                  ( < 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( not 
                     ( is-cargo 
                        "Charged" 
                        "<argument>" 
                        "Navigation" 
                     )
                  )
                  ( = ( mod ( mission-time ) 1 ) 0 ) 
               )
               ( set-weapon-energy 
                  ( + 
                     ( weapon-energy-pct "<argument>" ) 
                     2 
                  )
                  "<argument>" 
               )
            )
            ( when 
               ( and 
                  ( = 
                     ( weapon-energy-pct "<argument>" ) 
                     100 
                  )
                  ( is-cargo 
                     "Charging" 
                     "<argument>" 
                     "Navigation" 
                  )
                  ( = ( mod ( mission-time ) 3 ) 0 ) 
               )
               ( set-cargo 
                  "Charged" 
                  "<argument>" 
                  "Navigation" 
               )
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noname" 
         )
         ( when 
            ( not 
               ( = ( sim-hits-left "<argument>" ) 99 ) 
            )
            ( ship-maneuver 
               "<argument>" 
               0 
               0 
               0 
               0 
               ( false ) 
               0 
               0 
               300 
               ( true ) 
               2 
            )
         )
      )
      ( when 
         ( or 
            ( and 
               ( destroyed-or-departed-delay 
                  0 
                  "<argument>" 
               )
               ( destroyed-or-departed-delay 
                  0 
                  "<argument>" 
               )
            )
            ( = ( sim-hits-left "<argument>" ) 99 ) 
         )
         ( do-nothing ) 
      )
      ( when 
         ( true ) 
         ( when 
            ( < 
               ( distance "Alpha 1" "<argument>" ) 
               2500 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Weapons" 
               "Weapons" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Engines" 
               "Engine" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Main Beam" 
               "turret01" 
               "turret02" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Light Pulse" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "AAA Beam" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret33" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Beam Cannon" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Heavy Pulse" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Torpedo" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
            )
            ( lua-mark-subsystem 
               "@shipNameHolder[noname]" 
               "Missile System" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "noName" 
            )
         )
         ( when 
            ( > 
               ( distance "Alpha 1" "<argument>" ) 
               2499 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "<argument>" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "Weapons" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "Engine" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "turret01" 
               "turret02" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "turret19" 
               "turret20" 
               "turret21" 
               "turret22" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "turret29" 
               "turret30" 
               "turret31" 
               "turret32" 
               "turret33" 
               "turret34" 
               "turret35" 
               "turret36" 
               "turret33" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "turret03" 
               "turret04" 
               "turret05" 
               "turret06" 
               "turret07" 
               "turret08" 
               "turret09" 
               "turret10" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "turret11" 
               "turret12" 
               "turret13" 
               "turret14" 
               "turret15" 
               "turret16" 
               "turret17" 
               "turret18" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "Torpedo" 
               "turret23" 
               "turret24" 
               "turret25" 
               "turret26" 
               "turret27" 
               "turret28" 
            )
            ( lua-mark-clear-subsys 
               "@shipNameHolder[noname]" 
               "Missile System" 
               "turret63" 
               "turret64" 
               "turret65" 
               "turret66" 
            )
            ( modify-variable 
               "@shipNameHolder[noname]" 
               "noName" 
            )
         )
         ( modify-variable 
            "@shipNameHolder[noname]" 
            "noName" 
         )
      )
   )
   ( do-nothing ) 
   ( when-argument 
      ( every-of 
         "Hyperion" 
         "Diomedes" 
         "Hyperion B" 
         "Hyperion C" 
         "Deimos" 
         "Deimos B" 
         "Aeolus" 
         "Aeolus B" 
         "Aeolus C" 
         "Erebus" 
      )
      ( not ( targeted "<argument>" ) ) 
      ( hud-set-custom-gauge-active 
         ( false ) 
         "BPLowerRightMFD" 
         "BPLowerRightMFDA" 
         "BPLowerRightMFDB" 
         "BPLowerRightMFDC" 
         "BPLowerRightMFDD" 
         "BPLowerRightMFDE" 
         "BPLowerRightMFDF" 
         "BPLowerRightMFDG" 
         "BPLowerRightMFDH" 
      )
   )
)
+Name: BRAIN--Hyperion/Diomedes/Erebus
+Repeat Count: -1
+Trigger Count: 99999999
+Interval: 1
```