
--[[ 
    W3KEND | AUTO BHOP + INFINITE JUMP
    StarterPlayer > StarterPlayerScripts > LocalScript
]]

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local holdingSpace = false
local autoBhop = false
local infiniteJumpEnabled = false
local menuOpen = false
local animating = false
local humanoid

-- Upload your eyes image to Roblox and insert its asset ID.
local EYES_IMAGE = "rbxassetid://ТВОЙ_ID"

-- CHARACTER
local function setupCharacter(character)
    humanoid = character:WaitForChild("Humanoid")
end

if player.Character then
    setupCharacter(player.Character)
end

player.CharacterAdded:Connect(setupCharacter)

-- GUI
local gui = Instance.new("ScreenGui")
gui.Name = "W3KEND_AutoBhop"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.DisplayOrder = 50
gui.Parent = playerGui

local frame = Instance.new("Frame")
frame.Name = "Main"
frame.Size = UDim2.fromOffset(270, 235)
frame.Position = UDim2.new(0, 25, 0.5, -117)
frame.BackgroundColor3 = Color3.fromRGB(5, 5, 5)
frame.BackgroundTransparency = 1
frame.BorderSizePixel = 0
frame.ClipsDescendants = true
frame.Visible = false
frame.Parent = gui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 12)
corner.Parent = frame

local scale = Instance.new("UIScale")
scale.Scale = 0.8
scale.Parent = frame

local stroke = Instance.new("UIStroke")
stroke.Color = Color3.fromRGB(235, 235, 235)
stroke.Thickness = 1.5
stroke.Transparency = 1
stroke.Parent = frame

-- EYES BACKGROUND
local bg = Instance.new("ImageLabel")
bg.Name = "EyesBackground"
bg.Size = UDim2.fromScale(1, 1)
bg.BackgroundColor3 = Color3.fromRGB(8, 8, 8)
bg.BackgroundTransparency = 0
bg.Image = EYES_IMAGE
bg.ImageColor3 = Color3.fromRGB(220, 220, 220)
bg.ImageTransparency = 0.05
bg.ScaleType = Enum.ScaleType.Crop
bg.BorderSizePixel = 0
bg.ZIndex = 1
bg.Parent = frame

local bgCorner = Instance.new("UICorner")
bgCorner.CornerRadius = UDim.new(0, 12)
bgCorner.Parent = bg

-- DARK OVERLAY
local overlay = Instance.new("Frame")
overlay.Name = "DarkOverlay"
overlay.Size = UDim2.fromScale(1, 1)
overlay.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
overlay.BackgroundTransparency = 0.55
overlay.BorderSizePixel = 0
overlay.ZIndex = 2
overlay.Parent = frame

local overlayCorner = Instance.new("UICorner")
overlayCorner.CornerRadius = UDim.new(0, 12)
overlayCorner.Parent = overlay

-- TITLE
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -24, 0, 30)
title.Position = UDim2.fromOffset(12, 8)
title.BackgroundTransparency = 1
title.Text = "W3KEND  /  MOVEMENT"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextTransparency = 1
title.Font = Enum.Font.GothamBold
title.TextSize = 14
title.TextXAlignment = Enum.TextXAlignment.Left
title.ZIndex = 3
title.Parent = frame

-- DIVIDER
local line = Instance.new("Frame")
line.Size = UDim2.new(1, -24, 0, 1)
line.Position = UDim2.fromOffset(12, 42)
line.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
line.BackgroundTransparency = 1
line.BorderSizePixel = 0
line.ZIndex = 3
line.Parent = frame

-- AUTO BHOP BUTTON
local toggle = Instance.new("TextButton")
toggle.Name = "BhopToggle"
toggle.Size = UDim2.new(1, -24, 0, 38)
toggle.Position = UDim2.fromOffset(12, 53)
toggle.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
toggle.BackgroundTransparency = 1
toggle.Text = "AUTO BHOP  [ OFF ]"
toggle.TextColor3 = Color3.fromRGB(255, 255, 255)
toggle.TextTransparency = 1
toggle.Font = Enum.Font.GothamBold
toggle.TextSize = 12
toggle.AutoButtonColor = false
toggle.ZIndex = 3
toggle.Parent = frame

local toggleCorner = Instance.new("UICorner")
toggleCorner.CornerRadius = UDim.new(0, 7)
toggleCorner.Parent = toggle

local buttonStroke = Instance.new("UIStroke")
buttonStroke.Color = Color3.fromRGB(210, 210, 210)
buttonStroke.Transparency = 0.4
buttonStroke.Parent = toggle

-- INFINITE JUMP BUTTON
local infiniteButton = Instance.new("TextButton")
infiniteButton.Name = "InfiniteJumpToggle"
infiniteButton.Size = UDim2.new(1, -24, 0, 38)
infiniteButton.Position = UDim2.fromOffset(12, 100)
infiniteButton.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
infiniteButton.BackgroundTransparency = 1
infiniteButton.Text = "INFINITE JUMP  [ OFF ]"
infiniteButton.TextColor3 = Color3.fromRGB(255, 255, 255)
infiniteButton.TextTransparency = 1
infiniteButton.Font = Enum.Font.GothamBold
infiniteButton.TextSize = 12
infiniteButton.AutoButtonColor = false
infiniteButton.ZIndex = 3
infiniteButton.Parent = frame

local infiniteCorner = Instance.new("UICorner")
infiniteCorner.CornerRadius = UDim.new(0, 7)
infiniteCorner.Parent = infiniteButton

local infiniteStroke = Instance.new("UIStroke")
infiniteStroke.Color = Color3.fromRGB(180, 180, 180)
infiniteStroke.Transparency = 0.4
infiniteStroke.Parent = infiniteButton

-- FOOTER
local footer = Instance.new("TextLabel")
footer.Size = UDim2.new(1, 0, 0, 22)
footer.Position = UDim2.new(0, 0, 1, -25)
footer.BackgroundTransparency = 1
footer.Text = "B Y   W 3 K E N D"
footer.TextColor3 = Color3.fromRGB(230, 230, 230)
footer.TextTransparency = 1
footer.Font = Enum.Font.GothamMedium
footer.TextSize = 10
footer.ZIndex = 3
footer.Parent = frame

-- ANIMATION
local function animate(object, duration, properties)
    local tween = TweenService:Create(
        object,
        TweenInfo.new(
            duration,
            Enum.EasingStyle.Quint,
            Enum.EasingDirection.Out
        ),
        properties
    )
    tween:Play()
    return tween
end

-- OPEN MENU
local function openMenu()
    if menuOpen or animating then return end

    menuOpen = true
    animating = true
    frame.Visible = true
    frame.Position = UDim2.new(0, 25, 0.5, -97)
    frame.BackgroundTransparency = 1
    scale.Scale = 0.8

    animate(frame, 0.3, {
        Position = UDim2.new(0, 25, 0.5, -117),
        BackgroundTransparency = 0
    })

    animate(scale, 0.35, {Scale = 1})
    animate(stroke, 0.3, {Transparency = 0})
    animate(title, 0.25, {TextTransparency = 0})
    animate(line, 0.25, {BackgroundTransparency = 0.15})
    animate(toggle, 0.25, {
        BackgroundTransparency = 0.05,
        TextTransparency = 0
    })
    animate(infiniteButton, 0.25, {
        BackgroundTransparency = 0.05,
        TextTransparency = 0
    })
    animate(footer, 0.3, {TextTransparency = 0.05})

    task.delay(0.4, function()
        animating = false
    end)
end

-- CLOSE MENU
local function closeMenu()
    if not menuOpen or animating then return end

    menuOpen = false
    animating = true

    animate(frame, 0.2, {
        Position = UDim2.new(0, 25, 0.5, -90),
        BackgroundTransparency = 1
    })

    animate(scale, 0.2, {Scale = 0.82})
    animate(stroke, 0.15, {Transparency = 1})
    animate(title, 0.12, {TextTransparency = 1})
    animate(line, 0.12, {BackgroundTransparency = 1})
    animate(toggle, 0.12, {
        BackgroundTransparency = 1,
        TextTransparency = 1
    })
    animate(infiniteButton, 0.12, {
        BackgroundTransparency = 1,
        TextTransparency = 1
    })
    animate(footer, 0.12, {TextTransparency = 1})

    task.delay(0.22, function()
        frame.Visible = false
        animating = false
    end)
end

-- UPDATE BHOP BUTTON
local function updateBhopUI()
    if autoBhop then
        toggle.Text = "AUTO BHOP  [ ON ]"
        toggle.BackgroundColor3 = Color3.fromRGB(240, 240, 240)
        toggle.TextColor3 = Color3.fromRGB(0, 0, 0)
        buttonStroke.Color = Color3.fromRGB(255, 255, 255)
    else
        toggle.Text = "AUTO BHOP  [ OFF ]"
        toggle.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
        toggle.TextColor3 = Color3.fromRGB(255, 255, 255)
        buttonStroke.Color = Color3.fromRGB(180, 180, 180)
    end
end

-- UPDATE INFINITE JUMP BUTTON
local function updateInfiniteUI()
    if infiniteJumpEnabled then
        infiniteButton.Text = "INFINITE JUMP  [ ON ]"
        infiniteButton.BackgroundColor3 = Color3.fromRGB(240, 240, 240)
        infiniteButton.TextColor3 = Color3.fromRGB(0, 0, 0)
        infiniteStroke.Color = Color3.fromRGB(255, 255, 255)
    else
        infiniteButton.Text = "INFINITE JUMP  [ OFF ]"
        infiniteButton.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
        infiniteButton.TextColor3 = Color3.fromRGB(255, 255, 255)
        infiniteStroke.Color = Color3.fromRGB(180, 180, 180)
    end
end

toggle.Activated:Connect(function()
    autoBhop = not autoBhop
    updateBhopUI()
end)

infiniteButton.Activated:Connect(function()
    infiniteJumpEnabled = not infiniteJumpEnabled
    updateInfiniteUI()
end)

-- KEYBINDS
UIS.InputBegan:Connect(function(input, processed)
    if input.KeyCode == Enum.KeyCode.Insert then
        if menuOpen then
            closeMenu()
        else
            openMenu()
        end
    end

    if input.KeyCode == Enum.KeyCode.Space and not processed then
        holdingSpace = true
    end
end)

UIS.InputEnded:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.Space then
        holdingSpace = false
    end
end)

-- INFINITE JUMP
UIS.JumpRequest:Connect(function()
    if not infiniteJumpEnabled or not humanoid then
        return
    end

    if humanoid.Health > 0 then
        humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
    end
end)

-- AUTO BUNNY HOP
RunService.RenderStepped:Connect(function()
    if not autoBhop or not holdingSpace or not humanoid then
        return
    end

    if humanoid.Health > 0
        and humanoid.FloorMaterial ~= Enum.Material.Air then
        humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
    end
end)

updateBhopUI()
updateInfiniteUI()
openMenu()
