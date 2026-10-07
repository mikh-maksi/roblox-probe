# Add Score to Game

```lua
local function onPlayerJoin(player)
	local leaderstats = Instance.new("Folder")
	leaderstats.Name = "leaderstats"
	leaderstats.Parent = player

	local points = Instance.new("IntValue")
	points.Name = "Points"
	points.Value = 0
	points.Parent = leaderstats

end

game.Players.PlayerAdded:Connect(onPlayerJoin)

```


## Add Change Colors
```lua
while true do
	pointPart.Color = Color3.fromRGB(0, 0, 255)
	wait(4)
	pointPart.Color = Color3.fromRGB(0, 255, 0)
	wait(3)
	pointPart.Color = Color3.fromRGB(255 ,0, 0)
	wait(2)
	pointPart.BrickColor=BrickColor.new("Cool yellow")
	wait(2)
end
```
## Add Points
```lua
local pointPart = script.Parent
local Players = game:GetService("Players")


local function givePoints(player)	
	local playerStats = player:WaitForChild("leaderstats")	
	playerStats:WaitForChild("Points").Value +=  10	
	pointPart:Destroy()
end

local function partTouched(otherPart)
	local player = game.Players:GetPlayerFromCharacter(otherPart.Parent)
	if player then
		givePoints(player)
	end
end

pointPart.Touched:Connect(partTouched)

while true do
	pointPart.Color = Color3.fromRGB(0, 0, 255)
	wait(4)
	pointPart.Color = Color3.fromRGB(0, 255, 0)
	wait(3)
	pointPart.Color = Color3.fromRGB(255 ,0, 0)
	wait(2)
	pointPart.BrickColor=BrickColor.new("Cool yellow")
	wait(2)
end
```

## Add Points with BadaBoom
```lua
local pointPart = script.Parent

local blue = Color3.fromRGB(0, 0, 255)
local green = Color3.fromRGB(0, 255, 0)
local red = Color3.fromRGB(255 ,0, 0)
local yellow = Color3.fromRGB(255 ,255, 0)

local Players = game:GetService("Players")


local function givePoints(player)	
	local playerStats = player:WaitForChild("leaderstats")	
	playerStats:WaitForChild("Points").Value +=  10	
	pointPart:Destroy()
end

local function partTouched(otherPart)
	local player = game.Players:GetPlayerFromCharacter(otherPart.Parent)
	if player then
		givePoints(player)
	end
end

pointPart.Touched:Connect(partTouched)

while true do
	pointPart.Color = green
	wait(4)
	pointPart.Color = yellow
	Instance.new("Fire").Parent = pointPart
	wait(3)
	pointPart.Color = red
	Instance.new("Explosion").Parent = pointPart
	wait(2)
	pointPart.Fire:Destroy()
end

```
**Position**
```lua
wait(2)
while(true) do
	wait(0.1)
	script.Parent.Position = Vector3.new(200.742, 9.598, -257.211)
	wait(0.1)
	script.Parent.Position = Vector3.new(200.742, 9.598, -258.211)
	wait(0.1)
	script.Parent.Position = Vector3.new(200.742, 9.598, -259.211)
	wait(0.1)
	script.Parent.Position = Vector3.new(200.742, 9.598, -260.211)
	wait(0.1)
	script.Parent.Position = Vector3.new(200.742, 9.598, -261.211)
	wait(0.1)
	script.Parent.Position = Vector3.new(200.742, 9.598, -262.211)
	wait(0.1)
	script.Parent.Position = Vector3.new(200.742, 9.598, -270.211)
	wait(0.1)
	script.Parent.Position = Vector3.new(200.742, 9.598, -280.211)
	wait(0.1)
	script.Parent.Position = Vector3.new(200.742, 9.598, -290.211)
	wait(0.1)
	script.Parent.Position = Vector3.new(200.742, 9.598, -300.211)
end
```

