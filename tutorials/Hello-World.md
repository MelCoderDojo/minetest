# Hello World

# Hello World

```Lua
minetest.register_tool("tutorial:hellopick", {
	inventory_image = "tutorial_tool_hellopick.png",
})
```

Made like Stone Pickaxe, plus Hello World output.
```Lua
minetest.register_tool("tutorial:hellopick", {
	inventory_image = "tutorial_tool_hellopick.png",
	description = "Hello World Pickaxe",
	tool_capabilities = {
		full_punch_interval = 1.3,
		max_drop_level=0,
		groupcaps={
			cracky = {times={[2]=2.0, [3]=1.20}, uses=20, maxlevel=1},
		},
		damage_groups = {fleshy=3},
	},
	after_use = function(itemstack, user, node, digparams)      
	      minetest.chat_send_all("Hello world!")
         itemstack:add_wear(digparams.wear)
         return itemstack
      end,
})
```
Crafting Hello World Pickaxe. `default:` is needed for Minimal version, whereas `group:` in the regular one allows for all of the type instead of just the individual kind. (Cobblestone is a kind of stone, for instance.)

```Lua
minetest.register_craft({
	output = "tutorial:hellopick",
	recipe = {
		{'default:stone', 'default:dirt', 'default:stone'},
		{'', 'default:stick', ''},
		{'', 'default:stick', ''},
	}
})
```

```Lua
function tutorial_crafting()
   local s = "default:stone"
   local t = "default:stick"
   local d = "default:dirt"

   minetest.register_craft({
	   output = "tutorial:hellopick",
	   recipe = {
		   {s, d, s},
		   {'', t, ''},
		   {'', t, ''},
	   }
   })
end

tutorial_crafting()
```
