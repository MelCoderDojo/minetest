# Hello World

HUD stuff

```Lua
minetest.register_on_joinplayer(function(player)
     local hud_id = player:hud_add({
         hud_elem_type = 'text',
         text = 'First text',
         number = 0xFFFFFF,
         position = {x=0, y=1},
         alignment = {x=1, y=-1},
         offset = {x=4, y=-4}
     })
end)
```
