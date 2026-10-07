```lua
local function boom()
	exp = Instance.new("Explosion")	
	exp.Position = Workspace.Part.Position
	exp.Parent = Workspace
end

script.Parent.Activated:Connect(boom)

```
