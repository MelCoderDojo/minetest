## Introduction

As to tradition, we're going to start learning how to mod Minetest with "Hello world!" However, we're going to do it a bit differently. We're going to start by making a Hello World Pickaxe. Are you ready?

## Where?

To mod in Minetest, we have to put our files in the right spot.

 * Windows: `minetest-install-path/mods`
 * OS X: `minetest.app/Contents/Resources/bin/mods`
 * GNU/Linux: `~/.minetest/mods`

The Windows' location depends on where you installed it. Whatever you're using, just ask if you need help.

When you first start, the `mods` folder won't exist. You'll have to make it. Just make a new folder and name it `mods`.

## Setting Up

With the `mods` folder ready, we can start with our special pickaxe mod. We have to make our project have its own folder and get the parts for it all together.

1. Make a new folder inside of `mods`. Name it `helloworld`.
2. Inside of the new `helloworld` folder, we make a new file named `init.lua`
3. Make a new folder next to your file. Name it `textures`.
4. Save this `helloworld_hellopick.png` image into the `textures` folder.

This is the basic setup we need for this mod we're making. We gave it its own folder, `helloworld`, and then we setup the pieces it will use. `init.lua` is the file we will put our code in. The `textures` folder will hold our image for our pickaxe, that image being `helloworld_hellopick.png`.

## First Code

Open up `init.lua` in your editor.

```Lua
minetest.register_tool("helloworld:pick_hello", {
   inventory_image = "helloworld_hellopick.png",
})
```

Notice that there are parenthesis (`( )`) and braces (`{ }`). It might help to see it this way instead.

```Lua
minetest.register_tool("helloworld:pick_hello",
   {
      inventory_image = "helloworld_hellopick.png",
   }
)
```

When you've copied it down just like that, save the file.

## Trying the Pick

Let's check out our Hello Pickaxe now! Start up Minetest.

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
