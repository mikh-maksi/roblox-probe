# Task
`ServerScriptService`
--Изменяем цвет куба
game.Workspace.Part.BrickColor = BrickColor.new(0.9,0.6,0.2)
game.Workspace.Part.BrickColor = BrickColor.new(0.2,0.6,0.2)
game.Workspace.Part.BrickColor = BrickColor.new(0.8,0.2,0.8)


total = 0
function printFood()
	print("Curry!")
	total = 1
end

printFood()

# Task2
`FirePart`
local firePart = script.Parent

local function stopFire()
	wait(2)
	-- Destroy the fire instance
	firePart.Fire:Destroy()
	-- Add a new particle instance to the part
	local spark = Instance.new("ParticleEmitter")
	spark.Parent = firePart
	wait(3)
	--firePart:Destroy()
	
end
local function destroyBlock()
	firePart:Destroy()
end


wait(3)
stopFire()
wait(3)
destroyBlock()
# Task3
`Part`

local loopingPart = script.Parent

while true do
	loopingPart.BrickColor = BrickColor.new(0.9,0.6,0.2)
	wait(3)
	loopingPart.BrickColor = BrickColor.new(0.2,0.6,0.2)
	wait(3)
end

# Task4
`Part`

local loopingPart = script.Parent

while true do
	loopingPart.BrickColor = BrickColor.new(0.9,0.6,0.2)
	wait(3)
	loopingPart.BrickColor = BrickColor.new(0.2,0.6,0.2)
	wait(3)
end
# Task5
`Base Block Yellow (trap)`
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

total = 0


# Task6
`Base Block Red (trap)`

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
# Task7

