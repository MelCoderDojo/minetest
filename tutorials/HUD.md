# HUD Stuff

Originally from Hello-World.md. Splitting and saving this for later.

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
