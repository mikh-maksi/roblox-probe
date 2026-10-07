# Trial lesson: Game Development track
## When launching Roblox Studio, select the "Classic Baseplate" template.
<img src = "img/RobloxStudio1.jpg">

## The main workspace opens.
<img src = "img/RobloxStudio2.jpg">

## Select the Part item and the Block sub-item.
<img src = "img/RobloxStudio3.jpg">

## A rectangular block will be created.
<img src = "img/RobloxStudio4.jpg">

## In the Explorer menu block, click the plus sign.
<img src = "img/RobloxStudio5.jpg">

## And select the Script item.
<img src = "img/script.jpg">

## Click on the created Script element and delete the `print("Hello world!")` code.

<img src = "img/RobloxStudio7.jpg">

## Let's insert the code and run it.

```lua
element = script.Parent
element.BrickColor = BrickColor.new("Dark blue")
```
<img src = "img/RobloxStudio8.jpg">

## Let's see the result: after startup, the block turns dark blue.

<img src = "img/RobloxStudio9.jpg">

## Let's add a fire effect to the Part block.
To do this, click the "+" next to the block name (Part).
<img src = "img/RobloxStudio10.jpg">

And using the search function, we'll find the fire effect.
<img src = "img/RobloxStudio11.jpg">

Fire, as a property, appears on the selected block.
<img src = "img/RobloxStudio12.jpg">

## Let's add code that will dynamically change the effect.
```lua
local element = script.Parent

local function stopFire()
	element.Fire:Destroy()
	local spark = Instance.new("ParticleEmitter")
	spark.Parent = element
end

wait(10)
stopFire()
```
<img src = "img/RobloxStudio13.jpg">
Ten seconds after startup, this code will change the block's effect from fire to a particle emitter (ParticleEmitter).
<img src = "img/change_property.gif">  

## Let's add the implementation for the block disappearing.
To do this, we will create a `destroyBlock` function and call it 5 seconds after the "particle emitter" effect disappears.
```lua
local element = script.Parent

local function stopFire()
	element.Fire:Destroy()
	local spark = Instance.new("ParticleEmitter")
	spark.Parent = element
end
local function destroyBlock()
	element:Destroy()
end


wait(10)
stopFire()
wait(5)
destroyBlock()
```  
<img src = "img/RobloxStudio14.jpg">
отримаємо результат: 
<img src = "img/effects.gif">

## Let's add a special feature to the block: a cyclic color change.
```lua
while true do
	element.BrickColor = BrickColor.new(0.9,0.6,0.2)
	wait(3)
	element.BrickColor = BrickColor.new(0.2,0.6,0.2)
	wait(3)
end

```
<img src = "img/RobloxStudio15.jpg">
We will get the result.
<img src = "img/change_color.gif">

## Let's add point functionality.
Click "+" next to the "Workspace" item.
<img src = "img/RobloxStudio16.jpg">  
Select the Script item.
<img src = "img/RobloxStudio17.jpg">

In the newly created Script block, delete the `print("Hello world!")` code (which is there by default). Then, add the code for generating points:

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
<img src = "img/RobloxStudio18.jpg">
## Let's add a new block.
Select the Block button (1) on the toolbar. Choose Part (2) from the drop-down list. A new block (3) will be created.

<img src = "img/RobloxStudio19.jpg">
In the Explorer pane, click the "+" element next to the "Part" menu item corresponding to the created block.
<img src = "img/RobloxStudio20.jpg">
In the menu that appears, select the Script option.

<img src = "img/RobloxStudio21.jpg">

Instead of the default code in this block (`print("Hello world!")`), let's add code to award points based on the block's color.
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
	local player = game.Players:GetPlayerFromCharacter(otherPart.Parent)

	if player then
		givePoints(player)
	end
end

pointPart.Touched:Connect(partTouched)

while true do
	pointPart.Color = blue
	wait(4)
	pointPart.Color = green
	wait(3)
	pointPart.Color = red
	wait(2)
end
```
<img src = "img/RobloxStudio22.jpg">
Duplicate the block (by right-clicking on it and selecting "Duplicate").
<img src = "img/RobloxStudio23.jpg">
Move the duplicated block.
<img src = "img/duplicate.gif">
Repeat three times.

## Run the code to get the result.
<img src = "img/result.gif">
