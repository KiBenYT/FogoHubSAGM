local redzlib = loadstring(game:HttpGet("https://raw.githubusercontent.com/SrDark222/Mafia-hub-v1/refs/heads/main/mafia%20hub.lua"))()

-- window
local Window = redzlib:MakeWindow({
    Title = "Fogo Hub - Send A Global Message",
    SubTitle = "by KiBenBlox",
    SaveFolder = "fogo_hub.lua"
})

Window:AddMinimizeButton({
    Button = { Image = "rbxassetid://86046626374263", BackgroundTransparency = 0 },
    Corner = { CornerRadius = UDim.new(0.4, 1) }
})

local Tab1 = Window:MakeTab({"Principal", "home"})
Window:SelectTab(Tab1)

local AutoWinToggle = false
local AutoFarmToggle = false
local AntiAFKToggle = false

Tab1:AddToggle({
    Name = "Anti AFK",
    Description = "Impede o kick por inatividade",
    Default = false,
    Callback = function(Value)
        AntiAFKToggle = Value
        if Value then
            spawn(function()
                local vu = game:GetService("VirtualUser")
                while AntiAFKToggle do
                    task.wait(120)
                    if AntiAFKToggle then
                        vu:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
                        task.wait(0.1)
                        vu:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
                    end
                end
            end)
        end
    end
})

-- Auto Win Insane
Tab1:AddToggle({
    Name = "Auto Win Insane Obby",
    Description = "Teleporta pra ganhar o Insane Obby automaticamente",
    Default = false,
    Callback = function(Value)
        AutoWinToggle = Value
        local plr = game.Players.LocalPlayer
        if Value then
            spawn(function()
                local char = plr.Character or plr.CharacterAdded:Wait()
                while AutoWinToggle and char.Parent do
                    if char:FindFirstChild("HumanoidRootPart") then
                        char.HumanoidRootPart.Position = Vector3.new(135.8, 938.1, -335.95)
						wait(11.3)
                    end
                end
            end)
        else
            -- respawn quando desativa
            if plr.Character then
                plr.Character:BreakJoints()
            end
        end
    end
})

-- Auto Farm Orb
Tab1:AddToggle({
    Name = "Auto Farm Orb",
    Description = "Teleporta pra todas as orbs automaticamente",
    Default = false,
    Callback = function(Value)
        AutoFarmToggle = Value
        local player = game.Players.LocalPlayer
        if Value then
            spawn(function()
                local character = player.Character or player.CharacterAdded:Wait()
                local hrp = character:WaitForChild("HumanoidRootPart")
                local orbs = workspace:WaitForChild("Main"):WaitForChild("Orb"):WaitForChild("Orbs")
                while AutoFarmToggle and character.Parent do
                    for _, part in pairs(orbs:GetChildren()) do
                        if not AutoFarmToggle then break end
                        if part:IsA("BasePart") and string.find(part.Name, "Part") then
                            hrp.CFrame = part.CFrame + Vector3.new(0, 2, 0)
                            wait(0.3)
                        end
                    end
                    wait(0.3)
                end
            end)
        else
            -- respawn quando desativa
            if player.Character then
                player.Character:BreakJoints()
            end
        end
    end
})

Tab1:AddButton({"Win todos os Obbys", function(Value)
	local plr = game.Players.LocalPlayer
	local char = plr.Character or plr.CharacterAdded:Wait()
	local hrp = char.HumanoidRootPart

	task.wait(10)
	hrp.Position = Vector3.new(135.79998779296875, 939, -335.6999816894531)

	task.wait(10)
	hrp.Position = Vector3.new(87.99999237060547, 879, -415.5)

	task.wait(10)
	hrp.Position = Vector3.new(37.99999237060547, 879, -337.5)

	task.wait(10)
	hrp.Position = Vector3.new(-12.000007629394531, 879, -263.5)

	task.wait(10)
	hrp.Position = Vector3.new(-62.00000762939453, 879, -244.49998474121094)

	wait(0.3)
	char:BreakJoints()
end})
