local button = script.Parent
local panel = button.Parent
local player = game.Players.LocalPlayer
local uis = game:GetService("UserInputService")

panel.Visible = true
local infjumpActive = false

button.MouseButton1Click:Connect(function()
    panel.Visible = not panel.Visible
end)

uis.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    if input.UserInputType == Enum.UserInputType.Keyboard then
        if input.KeyCode == Enum.KeyCode.Space and infjumpActive then
            local character = player.Character
            if character and character:FindFirstChild("HumanoidRootPart") then
                character.HumanoidRootPart.Velocity = Vector3.new(
                    character.HumanoidRootPart.Velocity.X,
                    50, -- Fuerza del salto, ajustable
                    character.HumanoidRootPart.Velocity.Z
                )
            end
        end
    end
end)

panel:GetPropertyChangedSignal("Visible"):Connect(function()
    infjumpActive = panel.Visible
end)
