## Колір елементу - задаємо програмно

`ServerScriptService`

```lua
element = script.Parent
element.BrickColor = BrickColor.new(0.9,0.6,0.2)

```

## 2. Додаємо властивість - вогонь.

```lua
local element = script.Parent

local function stopFire()
	element.Fire:Destroy()
	local spark = Instance.new("ParticleEmitter")
	spark.Parent = element
	--element:Destroy()

end
local function destroyBlock()
	element:Destroy()
end


wait(3)
stopFire()
wait(3)
destroyBlock()
```

## 3. Задаємо унікальну особливість елементу - періодичну зміну кольору

`Part`

```lua
local element = script.Parent

while true do
	element.BrickColor = BrickColor.new(0.9,0.6,0.2)
	wait(3)
	element.BrickColor = BrickColor.new(0.2,0.6,0.2)
	wait(3)
end
```

# 4. При торканні блоку - він зникає

`Base Block Yellow (trap)`

```lua
local trap = script.Parent


-- Gets an object to destroy
local function onTouch(objectTouched)
	-- Destroy objectTouched
	print("Something touched the trap part")
	--objectTouched:Destroy()
	trap.BrickColor = BrickColor.new(0.9,0.6,0.2)
	wait(3)
	trap:Destroy()
	total +=1
	print(1)
end

-- Connects onTouch() to Touched event
trap.Touched:Connect(onTouch)
```

# 5. При торканні блоку - він вбиває

`Base Block Red (trap)`

```lua
local trap = script.Parent
trap.BrickColor = BrickColor.new(0.9,0,0)

-- Gets an object to destroy
local function onTouch(objectTouched)
	-- Destroy objectTouched
	print("Something touched the trap part")
	--objectTouched:Destroy()
	trap.BrickColor = BrickColor.new(0.9,0.6,0.2)
	wait(3)
	trap:Destroy()
	local character = objectTouched.Parent
	local humanoid = character:FindFirstChildWhichIsA("Humanoid")

	if humanoid then
		-- If part has humanoid, set health to 0
		humanoid.Health = 0
	end
end

-- Connects onTouch() to Touched event
trap.Touched:Connect(onTouch)
```

# 6. Додадаємо бали

До скрипту в корні

```lua
--In ServerScriptService, create a script named PlayerSetup with the contents below.

local function onPlayerJoin(player)
	local leaderstats = Instance.new("Folder")
	leaderstats.Name = "leaderstats"
	leaderstats.Parent = player

	-- Example of a IntValue
	local points = Instance.new("IntValue")
	points.Name = "Points"
	points.Value = 0
	points.Parent = leaderstats

end

-- Run onPlayerJoin when the PlayerAdded event fires
game.Players.PlayerAdded:Connect(onPlayerJoin)
```

До скрипту елементу

```lua
local pointPart = script.Parent

local blue = Color3.fromRGB(0, 0, 255)
local green = Color3.fromRGB(0, 255, 0)
local red = Color3.fromRGB(255 ,0, 0)

local smallPoints = 10
local largePoints = 50
local losePoints = 100

local Players = game:GetService("Players")

local function givePoints(player)
	local currentColor = pointPart.Color

	local playerStats = player:WaitForChild("leaderstats")
	local playerPoints = playerStats:WaitForChild("Points")

	if currentColor == blue then
		playerPoints.Value = playerPoints.Value + smallPoints
	elseif currentColor == green then
		playerPoints.Value = playerPoints.Value + largePoints
	else
		playerPoints.Value = playerPoints.Value - losePoints
	end


	pointPart:Destroy()

	local playerCharacter = player.Character
	local particle = Instance.new("ParticleEmitter")
	particle.Color = ColorSequence.new(currentColor)
	particle.Parent = playerCharacter:WaitForChild("Head")
	wait(1)
	particle:Destroy()

end



local function partTouched(otherPart)
	--local player = Players:GetPlayerFromCharacter(otherPart.Parent)
	local player = game.Players:GetPlayerFromCharacter(otherPart.Parent)

	if player then
		givePoints(player)
	end
end


pointPart.Touched:Connect(partTouched)


-- Changes the color of the part based on variables. Needs to be at bottom of script.
while true do
	pointPart.Color = blue
	wait(4)
	pointPart.Color = green
	wait(3)
	pointPart.Color = red
	wait(2)
end

```
