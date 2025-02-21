local library = loadstring(game:HttpGet("https://github.com/GoHamza/AppleLibrary/blob/main/main.lua?raw=true"))()

local window = library:init("Prison Life Script", true, Enum.KeyCode.RightShift, true)

window:Divider("Main")

local sectionA = window:Section("Troll")

sectionA:Divider("Troll")

sectionA:Button("Kill All (30 Secs)", function()
    spawn(function()
        local endTime = time() + 30

        while time() < endTime do
            for i, v in next, game:GetService("Players"):GetChildren() do
                pcall(function()
                    if v ~= game:GetService("Players").LocalPlayer and not v.Character:FindFirstChildOfClass("ForceField") and v.Character.Humanoid.Health > 0 then
                        local attackEndTime = time() + 30 - (endTime - time())
                        while v.Character:WaitForChild("Humanoid").Health > 0 and time() < attackEndTime do
                            wait();
                            game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = v.Character.HumanoidRootPart.CFrame;
                            for x, c in next, game:GetService("Players"):GetChildren() do
                                if c ~= game:GetService("Players").LocalPlayer then
                                    game.ReplicatedStorage.meleeEvent:FireServer(c)
                                end
                            end
                        end
                    end
                end)
                wait()
            end
        end
    end)
end)

sectionA:Button("NoClip", function()
    local Noclip = nil
    local Clip = nil
    local floatName = "Float"  -- Define floatName (it was missing)

    function noclip()
        Clip = false
        local function Nocl()
            if Clip == false and game.Players.LocalPlayer.Character ~= nil then
                for _, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
                    if v:IsA('BasePart') and v.CanCollide and v.Name ~= floatName then
                        v.CanCollide = false
                    end
                end
            end
            wait(0.21)
        end
        Noclip = game:GetService('RunService').Stepped:Connect(Nocl)
    end

    function clip()
        if Noclip then Noclip:Disconnect() end
        Clip = true
    end

    noclip()
end)

local sectionB = window:Section("TP")

sectionB:Divider("TP")

sectionB:Button("Get Guns (Cim Only)", function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local rootPart = character:WaitForChild("HumanoidRootPart")

    local targetCFrame = CFrame.new(-936.614441, 93.567009, 2056.45996, 0, -1, 0, 1, 0, -0, 0, 0, 1)

    local tweenService = game:GetService("TweenService")
    local tweenInfo = TweenInfo.new(
        1,
        Enum.EasingStyle.Linear,
        Enum.EasingDirection.Out,
        0,
        false,
        0
    )

    local tween = tweenService:Create(rootPart, tweenInfo, {CFrame = targetCFrame})
    tween:Play()
end)

sectionB:Button("Go To Jail", function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local rootPart = character:WaitForChild("HumanoidRootPart")

    local targetCFrame = CFrame.new(843.434937, 96.1383057, 2430.59375, -0.642763734, 0, -0.766064942, 0, 1, 0, 0.766064942, 0, -0.642763734)

    local tweenService = game:GetService("TweenService")
    local tweenInfo = TweenInfo.new(
        1,
        Enum.EasingStyle.Linear,
        Enum.EasingDirection.Out,
        0,
        false,
        0
    )

    local tween = tweenService:Create(rootPart, tweenInfo, {CFrame = targetCFrame})
    tween:Play()
end)


local sectionC = window:Section("Visuals")

sectionC:Divider("Visuals")

sectionC:Button("ESP", function()
    local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local function createESP(player)
    if player == LocalPlayer then return end

    local highlight = Instance.new("BoxHandleAdornment")

    -- ***Adjust these values to change the size***
    local boxWidth = 1.5  -- Adjust this (e.g., 1, 1.5, 2, etc.)
    local boxHeight = 5    -- Adjust this (e.g., 5, 6, 7, etc.)
    local boxDepth = 1.5  -- Adjust this (e.g., 1, 1.5, 2, etc.)

    highlight.Size = Vector3.new(boxWidth, boxHeight, boxDepth)
    highlight.Color3 = Color3.fromRGB(255, 0, 0)
    highlight.Transparency = 0.5
    highlight.AlwaysOnTop = true
    highlight.ZIndex = 5
    highlight.Adornee = nil
    highlight.Parent = game.CoreGui

    local function updateESP()
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            highlight.Adornee = player.Character.HumanoidRootPart
        else
            highlight.Adornee = nil
        end
    end

    local conn = RunService.RenderStepped:Connect(updateESP)

    player.CharacterAdded:Connect(updateESP)
    player.CharacterRemoving:Connect(function()
        highlight.Adornee = nil
    end)

    player.AncestryChanged:Connect(function()
        if not player:IsDescendantOf(game) then
            highlight:Destroy()
            conn:Disconnect()
        end
    end)

    -- Optional: Add a name tag above the head
    local nametag = Instance.new("BillboardGui")
    nametag.Size = UDim2.new(0, 100, 0, 20) -- Adjust size as needed
    nametag.StudsOffset = Vector3.new(0, 3, 0) -- Position above head
    nametag.Parent = player.Character or workspace -- Parent to character or workspace if character doesn't exist yet
    nametag.AlwaysOnTop = true

    local nameLabel = Instance.new("TextLabel")
    nameLabel.Text = player.Name
    nameLabel.Size = UDim2.new(1, 0, 1, 0)
    nameLabel.BackgroundTransparency = 1
    nameLabel.TextColor3 = Color3.fromRGB(255,255,255)
    nameLabel.Font = Enum.Font.SourceSansBold
    nameLabel.TextScaled = true
    nameLabel.Parent = nametag

    player.CharacterAdded:Connect(function(character)
        nametag.Parent = character
    end)

    player.CharacterRemoving:Connect(function()
        nametag.Parent = workspace -- or nil to remove completely
    end)
end


for _, player in ipairs(Players:GetPlayers()) do
    createESP(player)
end

Players.PlayerAdded:Connect(createESP)
end)

sectionC:Button("Aim Bot", function()
    loadstring(game:HttpGet("https://cdn.wearedevs.net/scripts/WRD%20Aimbot.txt"))()
 end)

game.StarterGui:SetCore("SendNotification", {Title = "Last Update Was", Text = "2/20/2025", Duration = 10})
