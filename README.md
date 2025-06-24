local plr = game.Players.LocalPlayer
local char = plr.Character or plr.CharacterAdded:Wait()

-- ScreenGui yaratish
local gui = Instance.new("ScreenGui")
gui.Name = "AbdullohGUI"
gui.Parent = plr:WaitForChild("PlayerGui")

-- Frame
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 220, 0, 250)
frame.Position = UDim2.new(0, 10, 0, 100)
frame.BackgroundColor3 = Color3.fromRGB(30,30,30)
frame.BorderSizePixel = 0

-- Tugma yaratish funksiyasi
local function createBtn(text, y)
    local btn = Instance.new("TextButton", frame)
    btn.Size = UDim2.new(1,0,0,40)
    btn.Position = UDim2.new(0,0,0,y)
    btn.BackgroundColor3 = Color3.fromRGB(60,60,60)
    btn.TextColor3 = Color3.new(1,1,1)
    btn.Text = text
    btn.Font = Enum.Font.SourceSansBold
    btn.TextSize = 20
    return btn
end

-- Tugmalar
local flyBtn     = createBtn("🚀 Fly", 0)
local speedBtn   = createBtn("🏃 Speed", 45)
local jumpBtn    = createBtn("🦘 Jump", 90)
local killBtn    = createBtn("💀 Kill Self", 135)
local explodeBtn = createBtn("💣 Explode", 180)

-- Funksiyalar
flyBtn.MouseButton1Click:Connect(function()
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if hrp and not hrp:FindFirstChild("FlyForce") then
        local bv = Instance.new("BodyVelocity", hrp)
        bv.Name = "FlyForce"
        bv.Velocity = Vector3.new(0, 50, 0)
        bv.MaxForce = Vector3.new(0, 100000, 0)
    end
end)

speedBtn.MouseButton1Click:Connect(function()
    char:FindFirstChildOfClass("Humanoid").WalkSpeed = 100
end)

jumpBtn.MouseButton1Click:Connect(function()
    char:FindFirstChildOfClass("Humanoid").JumpPower = 150
end)

killBtn.MouseButton1Click:Connect(function()
    char:FindFirstChildOfClass("Humanoid").Health = 0
end)

explodeBtn.MouseButton1Click:Connect(function()
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if hrp then
        local explosion = Instance.new("Explosion")
        explosion.Position = hrp.Position
        explosion.BlastRadius = 10
        explosion.BlastPressure = 500000
        explosion.Parent = workspace
    end
end)
