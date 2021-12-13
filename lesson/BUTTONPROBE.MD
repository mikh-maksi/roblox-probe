```lua
local button = script.Parent

local function onButtonActivated()
	Instance.new("Explosion").Parent = Workspace
end

button.Activated:Connect(onButtonActivated)
```
