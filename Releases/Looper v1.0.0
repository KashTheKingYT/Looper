--[[
https://kashthekingyt.github.io/looper

Looper is a module that allows you to easily loop functions without having to worry about lag or debounce. 
Leave regular while loops in the past with this more efficient module.

Creating a loop is as simple as:

local looper = require(game:GetService("ReplicatedStorage").Looper)
local loop = looper.loop(function() 
    print("Loop Ran")
end, 0)

]]

local looper = {}
looper.loops = {}

function looper.loop(Function, Delay, Name)
	if type(Function) == 'function' then
		
		local loop = {
			Function,
			Delay,
			false,
			true
		}
		
		function loop:Break()
			table.remove(looper.loops, table.find(looper.loops, loop))
		end
		
		function loop:TurnOff()
			loop[4] = false
		end
		
		function loop:TurnOn()
			loop[4] = true
		end
		
		looper.loops[Name or #looper.loops] = loop
		
		return loop
	else
		return false
	end
end

task.spawn(function()
	while true do
		for _,loop in pairs(looper.loops) do
			if not loop[3] and loop[4] then
				task.spawn(function()
					loop[3] = true
					loop[1]()
					wait(loop[2])
					loop[3] = false
				end)
			end
		end
		wait()
	end
end)

return looper
