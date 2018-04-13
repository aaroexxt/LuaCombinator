# LuaCombinator
This is a updated version of James OFarrell's original LuaCombinator Mod for Factorio.
You can download it at: https://mods.factorio.com/mod/LuaCombinator
Or, just copy the folder in this repo to your Factorio mods folder.
Thanks for downloading, and enjoy!

Text from mod page listing:
This is the 0.16 updated version of the LuaCombinator mod by James O'Farrell. Thanks to him for the idea and original mod! I really wanted this mod in 0.16 instead of 0.12, so I patched it!
Sorry that this took so long to update - I was busy with many other things.

This mod adds combinators which can execute lua scripts ingame. Use it however you want :)
If you have a problem, please leave a comment or bug report, I will get to it as soon as I can!

Some examples to get you started:
IMPORTANT: Make sure to set the combinator enabled condition, otherwise the combinator will not run.

-- floating text (no loop, repeat, post)
banner("Hello World", output.entity.position, {r=0,g=0,b=1},player)

--Wagon Inventory detector (no loop, repeat, post)
if (condition.value) then output:clear() for _,entity in pairs(entities) do ; if entity.name == "cargo-wagon" then inv = entity.get_inventory(1); for name,count in pairs(inv.get_contents()) do output:set_count("item",name,count); end end end elseif (not condition.value) then output:clear() end

--locomotive-detector (no loop, repeat, post)
if (condition.value) then output:clear() for _,entity in pairs(entities) do if entity.name == "diesel-locomotive" then output:set_count("item","diesel-locomotive",1) end end else output:clear() end

--locomotive pause(loop, repeat, post)
if entity.name == "diesel-locomotive" then entity.train.manual_mode = condition.value end

--rocket launch (loop, repeat)
if (entity.name == "rocket-silo") then player.print("lift off!"); entity.launch_rocket() end

--Power detector (no loop, repeat, post)
if (condition.value) then output:clear() for _,entity in pairs(entities) do if entity.type == "accumulator" then output:set_count("virtual","signal-E",math.floor(entity.energy/1000 + 0.5)) end end elseif not condition.value then output:clear() end

--lock the gate - signal (no loop, repeat, post)
output:clear(); for _,entity in pairs(entities) do if entity.name == "rail-signal" and entity.signal_state == 1 then output:set_count("item","rail-signal",1) end end

-- lock the gate- gate (loop, repeat, post)
if entity.name == "gate" then entity.active = not condition.value end

Disclaimer: If there is any problem with licensing or copyright I will take this down immediately. Please file a report if so. However, the original mod was listed as MIT Licensing (free to modify/publish), so it should be fine.

I am including the original comment here:

Using the Lua Combinator requires lua scripting knowledge. A good way to start with this mod is by basing away in the console and editing the examples.

The Lua Combinator will trigger a lua script when a logistics condition is met. It has option to repeat the script, to run it once after the condition changes and it to loop over entities.
This can be used for smart trains, accumulator, gates signals, roboports. logistics networks. Anything ht emod API can touch you can script with a Lua Combinator.
Repeat, will cause your command to run every half second
Post, run-once, will run your script once after the condition turns to false
Loop, will run your script once for every entity around it (in the 9x9 square)

Your script has access to the following variables (subject to change, sorry)

global: global table shared between all Lua Combinators
condition.value: the condition valu (true if it is met)
condition.changed: has the condition changed?
output: object to write to the wire network
output.entity:, constant-combinator entity
output:clear():, clear output
output:get_count(item): count of item
output:set_count(type,name,count): count of type name. see signals
state: persistent state of Lua Combinator
player: player who built combinator
game: factorio game object (have fun!)
entities: out of loop mode, this is the surrounding entities
entity: in loop mode, this is one of the surrounding entities

Original page: https://forums.factorio.com/viewtopic.php?f=93&t=15352

Enjoy :)
