This script's goal is to provide an enhanced system of capabilities for FS2 mission designers. It is based on prototype work done by General Battuta for Blue Planet; We want to create a system that makes capital ships more interesting to fight and gives them ways to respond to player action without a lot of manual scripting work by the mission designer.

Acknowledgments:
* General Battuta, for writing the initial scripts in the FS2 mission editor
* Axem, for AxemParse


This exposes the following new sexps:
* `brain-activate` _shipname_ 
   activates brain activity for the given ship if the ship class has a brain config
* `brain-deactivate` _shipname_
   turns the brain off
* `brain-force-behaviour` _shipname_ _number_
   Forces a ship to use a given behaviour pattern regardless of actual health
* `brain-get-behaviour-state` _shipname_
   Returns a number corresponding to the current preset
* `brain-get-drive-state` _shipname_
   Returns (Charging | Charged)
* `brain-get-weapon-state` _shipname_
   Returns current weapon fire rate
* `brain-get-repair-state` _shipname_
   Returns current state of the repair system

Configuration can be done through the brain-config.json file. 
This json defines a top-level dictionary, with its keys being class names (these must be the same as defined in ships.tbl). 
Presets have the following options:
`beam_turrets`: A list of strings with beam turret names. These turrets will follow the "Shuttering" behaviour, meaning that they will get temporary invulnerability and boosted repair rates after suffering a set amount of damage.
`presets`: A list of preset objects that define behaviours.