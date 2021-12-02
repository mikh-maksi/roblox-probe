```lua
local button = script.Parent

local function onButtonActivated()
	print("Button activated!")
	Instance.new("Explosion").Parent = Workspace
end

button.Activated:Connect(onButtonActivated)
```
