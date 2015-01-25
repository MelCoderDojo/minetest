# Hello World

HUD stuff

```Lua
minetest.register_on_joinplayer(function(player)
     local hud_id = player:hud_add({
         hud_elem_type = 'text',
         text = 'Hello world!',
         number = 0xFFFFFF,
         position = {x=0, y=1},
         alignment = {x=1, y=-1},
         offset = {x=4, y=-4}
     })
end)
```

Modify HUD text via formspec. Doesn't work in Minimal.

```Lua
-- Show form when the /formspec command is used.
minetest.register_chatcommand("formspec", {
	func = function(name, param)
		minetest.show_formspec(name, "tutorial:form",
				"size[4,3]" ..
				--"label[0,0;Hello, " .. name .. "]" ..
				"field[1,1.5;3,1;word;Enter name;]" ..
				"button_exit[1,2;2,1;exit;Save]")
	end
})

-- Register callback
minetest.register_on_player_receive_fields(function(player, formname, fields)
	if formname ~= "tutorial:form" then
		-- Formname is not mymod:form,
		-- exit callback.
		return false
	end

	-- Send message to player.
	changeText(player, fields.word)

	-- Return true to stop other minetest.register_on_player_receive_fields
	-- from receiving this submission.
	return true
end)

function changeText(player, word)
   local newString = "Hello, " .. word .. "!"
    player:hud_change(hold.hud_id, 'text', newString)
end
```


## Hello Pickaxe

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
