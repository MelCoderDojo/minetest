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
4. Save this little `helloworld_hellopick.png` image and put it in the `textures` folder:
![Hello Word Pickaxe](https://raw.githubusercontent.com/MelCoderDojo/minetest/draft/tutorials/tutorial_tool_hellopick.png)

This is the basic setup we need for this mod we're making. We gave it its own folder, `helloworld`, and then we setup the pieces it will use. `init.lua` is the file we will put our code in. The `textures` folder will hold our image for our pickaxe, that image being `helloworld_hellopick.png`.

## First Code

Open up `init.lua` in your editor.

```Lua
minetest.register_tool("helloworld:pick_hello", {
   inventory_image = "helloworld_hellopick.png"
})
```

Notice that there are parenthesis (`( )`) and braces (`{ }`). It might help to see it this way instead.

```Lua
minetest.register_tool
(
   "helloworld:pick_hello",
   {
      inventory_image = "helloworld_hellopick.png"
   }
)
```

When you've copied it down just like that, save the file.

## Trying the Pick

Let's check out our Hello Pickaxe now! Start up Minetest.

1. Hit *New* to make a new world to play in. Call it `Tutorial`.
2. Use the arrow keys (not the mouse) to select new world you made. Then hit *Configure*.
3. On the right-hand side, find our `helloworld` mod. Click on it.
4. Check the *enabled* box at the top.
5. Hit *Save*.

Now, start up the Tutorial world we just made!

We don't have a way to make our pickaxe, so we're going to tell the game to just give it to us.

1. Hit the **/** (slash) or **T** key.
2. Type in `/giveme helloworld:pick_hello`.
3. Hit **Enter** or press *Proceed*.

Now you have the Hello World Pickaxe!

If you notice, the `/giveme helloworld:pick_hello` matches some of the code we wrote earlier. That piece is basically the name the game calls our pickaxe.

If you wanted a Stone Pickaxe, you would instead do `/giveme default:pick_stone`. Just as we called ours with the name of our mod (`helloworld`), the regular tools have a name in front of them too (`default`).

## Item Description

Run around in the game and some other items. They can be other tools or just some blocks.

If you hit the **I** key and look at your items, you'll see that the other things all tell you what they are when the mouse arrow is over them. Our pickaxe doesn't do that. Let's fix that!

First, hit the **Esc** key and the *Exit to Menu* button. We'll play again soon, don't worry! We just can't change the code while the game is actually playing. It's okay while the start screen is up though.

So we need to add a line to our `init.lua`.

```Lua
minetest.register_tool("helloworld:pick_hello", {
   description = "Hello World Pickaxe",
   inventory_image = "helloworld_hellopick.png"
})
```

Again, if it's clearer, look at it this way.

```Lua
minetest.register_tool
(
   "helloworld:pick_hello",
   {
      description = "Hello World Pickaxe",
      inventory_image = "helloworld_hellopick.png"
   }
)
```

Make sure you don't forget that comma!

Once you get all that and save, start up the Tutorial world again. Check out your pickaxe in your item screen now. You did that!

## Adding More Properties

We need to give our pickaxe some more things. To help, let's look at the code for the Stone Pickaxe.

```Lua
minetest.register_tool("default:pick_stone", {
   description = "Stone Pickaxe",
   inventory_image = "default_tool_stonepick.png",
   tool_capabilities = {
      full_punch_interval = 1.3,
      max_drop_level=0,
      groupcaps={
         cracky = {times={[2]=2.0, [3]=1.20}, uses=20, maxlevel=1},
      },
      damage_groups = {fleshy=3},
   },
})
```

That's a lot of extra stuff! Let's copy the new things over into our Hello World Pickaxe code.

```Lua
minetest.register_tool("helloworld:pick_hello", {
   description = "Hello World Pickaxe",
   inventory_image = "helloworld_hellopick.png",
   tool_capabilities = {
      full_punch_interval = 1.3,
      max_drop_level=0,
      groupcaps={
         cracky = {times={[2]=2.0, [3]=1.20}, uses=20, maxlevel=1},
      },
      damage_groups = {fleshy=3},
   },
})
```
Just don't forget that comma! 
```Lua
inventory_image = "helloworld_hellopick.png",  -- Comma here!
```
So right now, our Hello World Pickaxe works like a Stone Pickaxe. What blocks it can break, how much damage it can do, all of that.

Go try it out and make sure your code works.

## Putting in Hello World

Being our first item and being called the Hello World Pickaxe could be considered good enough for some for a Hello World sort of thing. However, we're going to go one step further and actually make the words "Hello world!" come up from our tool.

```Lua
minetest.register_tool("helloworld:pick_hello", {
   description = "Hello World Pickaxe",
   inventory_image = "helloworld_hellopick.png",
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
   end
})
```

What's happening here is that we're changing what happens after using the pickaxe, that's why it's called `after_use`. In particular, for something like a pickaxe, that means after breaking a block.

In there, we add in our line for making the words "Hello world!" come out. The things after that are what normally happens in the `after_use` if we didn't change it like we are now.

Now, give it another go. Break some blocks and get "Hello world!" to come up. Fortunately, the comma was a nice extra that was already there from last time. Hopefully you don't have any other issues, but if you do, just compare your code to what's above.

## Craft the Pick

It doesn't really feel part of the game to have to use a sort of cheat code to get it. Let's make it so we can actually craft our pickaxe.

Just add in what's below with the rest of your code.

```Lua
minetest.register_craft({
	output = "helloworld:pick_hello",
	recipe = {
		{'default:cobble', 'default:dirt', 'default:cobble'},
		{'', 'default:stick', ''},
		{'', 'default:stick', ''},
	}
})
```

With this, we can craft the Hello World Pickaxe just like a regular Stone Pickaxe, just with a block of dirt at the top of the T shape.

With a few adjustments, we can make this shape a bit more clear.

```Lua
local c = "default:cobble"
local s = "default:stick"
local d = "default:dirt"

minetest.register_craft({
   output = "tutorial:hellopick",
   recipe = {
      {c, d, c},
      {'', s, ''},
      {'', s, ''},
   }
})
```

Can you see the pickaxe shape in the code a bit better now?

## You've Done It!

If everything is working right, congratulations! You've made your very first mod.
