local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/joeengo/exploiting/main/EngoUILIB_V2.lua", true))()

local main = library:CreateMain("Hybird.Ego Vault Set By YoltW#1051", "", Enum.KeyCode.LeftAlt)

local tab = main:CreateTab("Slient Tab")

tab:CreateLabel("Launched Streamable click Toggle and when executed only 1 one time dont untick or tick again will get error")

tab:CreateToggle("Toggle", function(value)
--["LuarmorKey"] = "YoltWTestKey",
getgenv().Hybird = {
    General = {
        Notifications = true,
        Intro = true, 
        FOVMode = "PredictionPoint"
    },
    Silent = {
        Main = {
            Enabled = true,
            Mode = "Target",
            Toggle = "Q",
            Prediction = 0.1155,
            Parts = {"Head", "UpperTorso", "HumanoidRootPart", "LowerTorso", "LeftHand", "RightHand", "LeftLowerArm", "RightLowerArm", "LeftUpperArm", "RightUpperArm", "LeftFoot", "LeftLowerLeg",  "LeftUpperLeg", "RightLowerLeg", "RightFoot",  "RightUpperLeg"}
        },
        FOV = {
            ShowFOV = false,
            Radius = 60,
            Color = Color3.fromRGB(0, 71, 171),
            Filled = false,
            Transparency = 0.8
        }
    },
    Camlock = {
        Main = {
            Enabled = true,
            Key = "C",
            UnlockKey = "Z",
            SmoothLock = true,
            Smoothness = 0.0292,
            PredictMovement = true,
            Prediction = 0.112,
            Shake = false,
            ShakeValue = 16.4,
            Parts = {"Head"}
        },
        FOV = {
            UseFOV = true,
            ShowFOV = false,
            Radius = 55,
            Color = Color3.fromRGB(0, 71, 171),
            Filled = false,
            Transparency = 0.4
        }
    },
    Tracer = {
        Enabled = false,
        Color = Color3.fromRGB(137, 207, 240),
        Transparency = 0.4,
        Visible = false
    },
    AutoPrediction = { -- Do NOT disable auto pred it will break ur script fixing next update
        Enabled = true,
        ping20_30 = 0.12588,
        ping30_40 = 0.11911,
        ping40_50 = 0.12471,
        ping50_60 = 0.12766,
        ping60_70 = 0.12731,
        ping70_80 = 0.12951,
        ping80_90 = 0.13181,
        ping90_100 = 0.138,
        ping100_110 = 0.146,
        ping110_120 = 0.1367,
        ping120_130 = 0.1401,
        ping130_140 = 0.1437,
        ping140_150 = 0.153,
        ping150_160 = 0.1514,
        ping160_170 = 0.1663,
        ping170_180 = 0.1672,
        ping180_190 = 0.1848,
        ping190_200 = 0.1865,
    },
    Key360 = {
        Toggle = false,
        RotationSpeed = 2500, -- higher you go the faster the spin. 2500 is good
        Keybind = Enum.KeyCode.L
    },
}
if Hybird.General.Intro then 
    local cam = workspace.CurrentCamera
    local x = cam.ViewportSize.X
    local y = cam.ViewportSize.Y
    local newx = math.floor(x * 0.5)
    local newy = math.floor(y * 0.5)

    local SpashScreen = Instance.new("ScreenGui")
    local Image = Instance.new("ImageLabel")
    SpashScreen.Name = "SpashScreen"
    SpashScreen.Parent = game.CoreGui
    SpashScreen.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    Image.Name = "Image"
    Image.Parent = SpashScreen
    Image.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    Image.BackgroundTransparency = 1
    Image.Position = UDim2.new(0, newx, 0, newy)
    Image.Size = UDim2.new(0, 793, 0, 392)
    Image.Image = "rbxassetid://14263663551"
    Image.ImageTransparency = 1
    Image.AnchorPoint = Vector2.new(0.5,0.5)

    local Blur = Instance.new("BlurEffect")
    Blur.Parent = game.Lighting
    Blur.Size = 0
    Blur.Name = math.random(1,123123)

    local function gui(last, sex, t, s, inorout)
        local TI = TweenInfo.new(t or 1, s or Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)
        local Tweening = game:GetService("TweenService"):Create(last, TI, sex)
        Tweening:Play()
    end

    gui(Image, {ImageTransparency = 0},0.3)
    gui(Blur, {Size = 150},0.3)
    wait(3)
    gui(Image, {ImageTransparency = 1},0.3)
    gui(Blur, {Size = 0},0.3)
    wait(0.3)
end

local function getnamecall()
    if game.PlaceId == 2788229376 then
        return "UpdateMousePos"
    elseif game.PlaceId == 5602055394 or game.PlaceId == 7951883376 then
        return "MousePos"
    elseif game.PlaceId == 9825515356 then
        return "GetMousePos"
    end
end

local namecalltype = getnamecall()

function MainEventLocate()
    for _,v in pairs(game:GetService("ReplicatedStorage"):GetDescendants()) do
        if v.Name == "MainEvent" then
            return v
        end
    end
end

-- 360 on bind made by prime >_<
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera
local Toggle = getgenv().Hybird.Key360.Toggle
local RotationSpeed = getgenv().Hybird.Key360.RotationSpeed
local Keybind = getgenv().Hybird.Key360.Keybind

local function OnKeyPress(Input, GameProcessedEvent)
    if Input.KeyCode == Keybind and not GameProcessedEvent then 
        Toggle = not Toggle
    end
end

UserInputService.InputBegan:Connect(OnKeyPress)

local LastRenderTime = 0
local FullCircleRotation = 2 * math.pi
local TotalRotation = 0

local function RotateCamera()
    if Toggle then
        local CurrentTime = tick()
        local TimeDelta = math.min(CurrentTime - LastRenderTime, 0.01)
        LastRenderTime = CurrentTime

        local Rotation = CFrame.fromAxisAngle(Vector3.new(0, 1, 0), math.rad(RotationSpeed * TimeDelta))
        Camera.CFrame = Camera.CFrame * Rotation

        TotalRotation = TotalRotation + math.rad(RotationSpeed * TimeDelta)
        if TotalRotation >= FullCircleRotation then
            Toggle = false
            TotalRotation = 0
        end
    end
end

RunService.RenderStepped:Connect(RotateCamera)


local mainevent = MainEventLocate()

-- // Shorthand
local uwuHybird = getgenv().Hybird
local uwuMain = uwuHybird.General
local uwuCamMain = uwuHybird.Camlock.Main
local uwuCamFOV = uwuHybird.Camlock.FOV
local uwuSilentMain = uwuHybird.Silent.Main
local uwuSilentFOV = uwuHybird.Silent.FOV
local uwuTrace = uwuHybird.Tracer
local uwuAutoPred = uwuHybird.AutoPrediction

-- // Optimization
local vect3 = Vector3.new
local vect2 = Vector2.new
local cnew = CFrame.new

-- // Libraries
local NotificationHolder = loadstring(game:HttpGet("https://raw.githubusercontent.com/BocusLuke/UI/main/STX/Module.Lua"))()
local Notification = loadstring(game:HttpGet("https://raw.githubusercontent.com/BocusLuke/UI/main/STX/Client.Lua"))()

-- // Services
local uis = game:GetService("UserInputService")
local rs = game:GetService("RunService")
local plrs = game:GetService("Players")
local ws = game:GetService("Workspace")

-- // Script Variables
local CToggle = false
local lplr = plrs.LocalPlayer
local CTarget = nil
local CPart = nil
local SToggle = false
local STarget = nil
local SPart = nil

-- // Client Variables
local m = lplr:GetMouse()
local c = ws.CurrentCamera

-- // Notification Function
local function SendNotification(text)
    Notification:Notify(
        {Title = "Hybird.Ego V4.0a", Description = "Hybird - "..text},
        {OutlineColor = Color3.fromRGB(255,255,255),Time = 2, Type = "image"},
        {Image = "http://www.roblox.com/asset/?id=14260342598", ImageColor = Color3.fromRGB(137,207,240)}
    )
end 

-- // Call notification function
if uwuMain.Notifications then
    SendNotification("Yoltw#1095 - inject Hybird.Ego V4.0a")
    wait(3.5)
    SendNotification("Made By YoltW, Esea2, Nonox, Mathi, and the guy suggest some feature is NVTH")
end

-- // Camlock FOV
local CamlockFOV = Drawing.new("Circle")
CamlockFOV.Visible = uwuCamFOV.ShowFOV
CamlockFOV.Thickness = 1
CamlockFOV.NumSides = 30
CamlockFOV.Radius = uwuCamFOV.Radius * 3
CamlockFOV.Color = uwuCamFOV.Color
CamlockFOV.Filled = uwuCamFOV.Filled
CamlockFOV.Transparency = uwuCamFOV.Transparency

--Silent FOV
local SilentFOV = Drawing.new("Circle")
SilentFOV.Visible = uwuSilentFOV.ShowFOV
SilentFOV.Thickness = 1
SilentFOV.NumSides = 30
SilentFOV.Radius = uwuSilentFOV.Radius * 3
SilentFOV.Color = uwuSilentFOV.Color
SilentFOV.Filled = uwuSilentFOV.Filled
SilentFOV.Transparency = uwuSilentFOV.Transparency

--Tracer
local Line = Drawing.new("Line")
Line.Color = uwuTrace.Color
Line.Transparency = uwuTrace.Transparency
Line.Thickness = 1
Line.Visible = uwuTrace.Visible

-- // Script Functions
local function uwuFindTawget() -- // Find target
    local d, t = math.huge, nil
    for _,v in pairs (plrs:GetPlayers()) do
        local _,os = c:WorldToViewportPoint(v.Character.PrimaryPart.Position)
        if v ~= lplr and v.Character and v.Character:FindFirstChild("Humanoid") and v.Character.Humanoid.Health ~= 0 and v.Character:FindFirstChild("HumanoidRootPart") and os then
            local pos = c:WorldToViewportPoint(v.Character.PrimaryPart.Position)
            local magnitude = (vect2(pos.X, pos.Y) - vect2(m.X, m.Y + 36)).magnitude
            if magnitude < d then
                t = v
                d = magnitude
            end
        end
    end
    return t
end

local function uwuFindPart() -- // Find aimpart
    local d, p = math.huge, nil
    if CTarget then
        for _,v in pairs(CTarget.Character:GetChildren()) do
            if table.find(uwuCamMain.Parts, v.Name) then
                local pos = c:WorldToViewportPoint(v.Position)
                local Magn = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
                if Magn < d then
                    d = Magn
                    p = v
                end
            end
        end
        return p.Name
    end
end

local function uwuFindSilentPart() -- // Find aimpart
    local d, p = math.huge, nil
    if CTarget then
        for _,v in pairs(CTarget.Character:GetChildren()) do
            if table.find(uwuSilentMain.Parts, v.Name) then
                local pos = c:WorldToViewportPoint(v.Position)
                local Magn = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
                if Magn < d then
                    d = Magn
                    p = v
                end
            end
        end
        return p.Name
    end
end

local function uwuCheckAnti(targ) -- // Anti-aim detection
    if (targ.Character.HumanoidRootPart.Velocity.Y < -5 and targ.Character.Humanoid:GetState() ~= Enum.HumanoidStateType.Freefall) or targ.Character.HumanoidRootPart.Velocity.Y < -50 then
        return true
    elseif targ and (targ.Character.HumanoidRootPart.Velocity.X > 35 or targ.Character.HumanoidRootPart.Velocity.X < -35) then
        return true
    elseif targ and targ.Character.HumanoidRootPart.Velocity.Y > 60 then
        return true
    elseif targ and (targ.Character.HumanoidRootPart.Velocity.Z > 35 or targ.Character.HumanoidRootPart.Velocity.Z < -35) then
        return true
    else
        return false
    end
end

local function InSilentRadiuwus(target, section, fov) -- // Check if player is in the fov
    if target then
        local pos = nil
        if not uwuCheckAnti(target) then
            pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + target.Character.PrimaryPart.Velocity * section.Prediction)
        else
            pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + ((target.Character.Humanoid.MoveDirection * target.Character.Humanoid.WalkSpeed) * section.Prediction))
        end
        local mag = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
        if mag < fov * 3 then
            return true
        else
            return false
        end
    end
end

local function Silent()
    if STarget then
        if SPart and InSilentRadiuwus(STarget, uwuSilentMain, SilentFOV.Radius) then
            if not uwuCheckAnti(STarget) then
                mainevent:FireServer(namecalltype, STarget.Character[SPart].Position + (STarget.Character[SPart].Velocity * uwuSilentMain.Prediction))
            else
                mainevent:FireServer(namecalltype, STarget.Character[SPart].Position + ((STarget.Character.Humanoid.MoveDirection * STarget.Character.Humanoid.WalkSpeed) * uwuSilentMain.Prediction))
            end
        end
    end
end


local function InRadiuwus(target, section, fov) -- // Check if player is in the fov
    if target then
        if uwuCamFOV.UseFOV then
            local pos = nil
            if not uwuCheckAnti(target) then
                pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + target.Character.PrimaryPart.Velocity * section.Prediction)
            else
                pos = c:WorldToViewportPoint(target.Character.PrimaryPart.Position + ((target.Character.Humanoid.MoveDirection * target.Character.Humanoid.WalkSpeed) * section.Prediction))
            end
            local mag = (vect2(m.X, m.Y + 36) - vect2(pos.X, pos.Y)).Magnitude
            if mag < fov * 3 then
                return true
            else
                return false
            end
        else
            return true
        end
    end
end

uis.InputBegan:Connect(function(k,t)
    if not t then
        if k.KeyCode == Enum.KeyCode[uwuCamMain.Key:upper()] then
            CToggle = true
            CTarget = uwuFindTawget()
            if uwuMain.Notifications then
                SendNotification("locked onto "..CTarget.Name)
            end
        elseif k.KeyCode == Enum.KeyCode[uwuCamMain.UnlockKey:upper()] then
            if CToggle then
                CToggle = false
                CTarget = nil
                if uwuMain.Notifications then
                    SendNotification("unlocked")
                end
            end
        elseif k.KeyCode == Enum.KeyCode[uwuSilentMain.Toggle:upper()] and uwuSilentMain == "Regular" then
            if SToggle then
                SToggle = false
                if uwuMain.Notifications then
                    SendNotification("silent disabled")
                end
            else
                SToggle = true
                if uwuMain.Notifications then
                    SendNotification("silent enabled")
                end
            end
        end
    end
end)

rs.RenderStepped:Connect(function()
    if CTarget then
        CPart = uwuFindPart()
        local pos = nil
        local cum = nil
        if CTarget.Character.BodyEffects["K.O"].Value == true or lplr.Character.BodyEffects["K.O"].Value == true then
            CToggle = false
            CTarget = nil
        else
            if uwuCamMain.Shake then
                if uwuCamMain.PredictMovement then
                    if not uwuCheckAnti(CTarget) then
                        cum = CTarget.Character[CPart].Position + CTarget.Character[CPart].Velocity * uwuCamMain.Prediction + (vect3(
                            math.random(-uwuCamMain.ShakeValue, uwuCamMain.ShakeValue),
                            math.random(-uwuCamMain.ShakeValue, uwuCamMain.ShakeValue),
                            math.random(-uwuCamMain.ShakeValue, uwuCamMain.ShakeValue)
                        ) * 0.1)
                    else
                        cum = CTarget.Character[CPart].Position + ((CTarget.Character.Humanoid.MoveDirection * CTarget.Character.Humanoid.WalkSpeed) * uwuCamMain.Prediction + (vect3(
                            math.random(-uwuCamMain.ShakeValue, uwuCamMain.ShakeValue),
                            math.random(-uwuCamMain.ShakeValue, uwuCamMain.ShakeValue),
                            math.random(-uwuCamMain.ShakeValue, uwuCamMain.ShakeValue)
                        ) * 0.1))
                    end
                    pos = c:WorldToViewportPoint(cum)
                else
                    cum = CTarget.Character[CPart].Position + (vect3(
                        math.random(-uwuCamMain.ShakeValue, uwuCamMain.ShakeValue),
                        math.random(-uwuCamMain.ShakeValue, uwuCamMain.ShakeValue),
                        math.random(-uwuCamMain.ShakeValue, uwuCamMain.ShakeValue)
                    ) * 0.1)
                    pos = c:WorldToViewportPoint(cum)
                end
            else
                if uwuCamMain.PredictMovement then
                    if not uwuCheckAnti(CTarget) then
                        cum = CTarget.Character[CPart].Position + CTarget.Character[CPart].Velocity * uwuCamMain.Prediction
                    else
                        cum = CTarget.Character[CPart].Position + ((CTarget.Character.Humanoid.MoveDirection * CTarget.Character.Humanoid.WalkSpeed) * uwuCamMain.Prediction)
                    end
                    pos = c:WorldToViewportPoint(cum)
                else
                    cum = CTarget.Character[CPart].Position
                    pos = c:WorldToViewportPoint(cum)
                end
            end
            if InRadiuwus(CTarget, uwuCamMain, CamlockFOV.Radius) then
                local main = nil
                if uwuCamMain.SmoothLock then
                    main = cnew(c.CFrame.p, cum)
                    c.CFrame = c.CFrame:Lerp(main, uwuCamMain.Smoothness, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)
                else
                    c.CFrame = cnew(c.CFrame.p, cum)
                end
            end
            if uwuMain.FOVMode == "Mouse" then
                if uwuCamFOV.ShowFOV then
                    CamlockFOV.Position = vect2(m.X, m.Y + 36)
                end
                if uwuSilentFOV.ShowFOV then
                    SilentFOV.Position = vect2(m.X, m.Y + 36)
                end
            elseif uwuMain.FOVMode == "PredictionPoint" then
                if uwuCamFOV.ShowFOV then
                    CamlockFOV.Position = vect2(pos.X, pos.Y)
                end
                if uwuSilentFOV.ShowFOV then
                    SilentFOV.Position = vect2(pos.X, pos.Y)
                end
            end
            if uwuTrace.Enabled then
                Line.Visible = true
                Line.From = vect2(m.X, m.Y + 36)
                Line.To = vect2(pos.X, pos.Y)
            end
        end
    else
        CamlockFOV.Position = vect2(m.X, m.Y + 36)
        SilentFOV.Position = vect2(m.X, m.Y + 36)
        Line.Visible = false
    end
end)

lplr.Character.ChildAdded:Connect(function(tool)
    if tool:IsA("Tool") then
        tool.Activated:connect(function()
            if uwuSilentMain.Mode == "Regular" then
                if SToggle then
                    STarget = uwuFindTawget()
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            elseif uwuSilentMain.Mode == "Target" then
                if CToggle then
                    STarget = CTarget
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            end
        end)
    end
end)

lplr.CharacterAdded:Connect(function(char)
    char.ChildAdded:Connect(function(tool)
        tool.Activated:connect(function()
            if uwuSilentMain.Mode == "Regular" then
                if SToggle then
                    STarget = uwuFindTawget()
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            elseif uwuSilentMain.Mode == "Target" then
                if CToggle then
                    STarget = CTarget
                    if STarget then
                        SPart = uwuFindSilentPart()
                        if SPart then
                            Silent()
                        end
                    end
                end
            end
        end)
    end)
end)

--Auto Prediction
coroutine.resume(coroutine.create(function()
    while true do
        if uwuAutoPred.Enabled then
            local ping = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]:GetValue()
            if ping <= 40 then
                uwuSilentMain.Prediction = uwuAutoPred.ping30_40
            elseif ping <= 50 then
                uwuSilentMain.Prediction = uwuAutoPred.ping40_50
            elseif ping <= 60 then
                uwuSilentMain.Prediction = uwuAutoPred.ping50_60
            elseif ping <= 70 then
                uwuSilentMain.Prediction = uwuAutoPred.ping60_70
            elseif ping <= 80 then
                uwuSilentMain.Prediction = uwuAutoPred.ping70_80
            elseif ping <= 90 then
                uwuSilentMain.Prediction = uwuAutoPred.ping80_90
            elseif ping <= 100 then
                uwuSilentMain.Prediction = uwuAutoPred.ping90_100
            elseif ping <= 110 then
                uwuSilentMain.Prediction = uwuAutoPred.ping100_110
            elseif ping <= 120 then
                uwuSilentMain.Prediction = uwuAutoPred.ping110_120
            elseif ping <= 130 then
                uwuSilentMain.Prediction = uwuAutoPred.ping120_130
            elseif ping <= 140 then
                uwuSilentMain.Prediction = uwuAutoPred.ping130_140
            elseif ping <= 150 then
                uwuSilentMain.Prediction = uwuAutoPred.ping140_150
            elseif ping <= 160 then
                uwuSilentMain.Prediction = uwuAutoPred.ping150_160
            elseif ping <= 170 then
                uwuSilentMain.Prediction = uwuAutoPred.ping160_170
            elseif ping <= 180 then
                uwuSilentMain.Prediction = uwuAutoPred.ping170_180
            elseif ping <= 190 then
                uwuSilentMain.Prediction = uwuAutoPred.ping180_190
            elseif ping <= 200 then
                uwuSilentMain.Prediction = uwuAutoPred.ping190_200
            end
            task.wait(0.7)
        end
    end
end))
end);
local tab = main:CreateTab("Games Setting")

tab:CreateLabel("Main")

tab:CreateToggle("Crosshair Changes", function(value)
--Crossair Change *leaked so i save 50 robux frrrrrr*
--[[
]]
game.Players.LocalPlayer.DataFolder.CursorImage.Value = 12825334563 --Dx9358239538727 Crosshair 
--[[
Yo haven't seen you long time dude I miss y'all

]]
print("Crosshair")
end);
local tab = main:CreateTab("Color Correction")

tab:CreateLabel("Main")

tab:CreateToggle("Color Correction", function(value)
local l = game:GetService("Lighting")

local col = Instance.new("ColorCorrectionEffect", l)
col.Brightness = 0
col.Contrast = 0.01
col.Saturation = 0.67   
end);
local tab = main:CreateTab("Fps Counter")

tab:CreateLabel("Main")

tab:CreateToggle("Fps Counter", function(value)
local FpsGui = Instance.new("ScreenGui")
local FPSAmount = Instance.new("TextLabel")
local RunService = game:GetService("RunService")
local TimeFunction = RunService:IsRunning() and time or os.clock

local LastIteration, Start
local FrameUpdateTable = {}

local function HeartbeatUpdate()
	LastIteration = TimeFunction()
	for Index = #FrameUpdateTable, 1, -1 do
		FrameUpdateTable[Index + 1] = FrameUpdateTable[Index] >= LastIteration - 1 and FrameUpdateTable[Index] or nil
	end

	FrameUpdateTable[1] = LastIteration
	FPSAmount.Text = tostring(math.floor(TimeFunction() - Start >= 1 and #FrameUpdateTable or #FrameUpdateTable / (TimeFunction() - Start)))
end

Start = TimeFunction()
RunService.Heartbeat:Connect(HeartbeatUpdate)

FpsGui.Name = "FpsGui"
FpsGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
FpsGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

FPSAmount.Name = "FPSAmount"
FPSAmount.Parent = FpsGui
FPSAmount.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
FPSAmount.BackgroundTransparency = 1.000
FPSAmount.Size = UDim2.new(0.150000006, 0, 0.100000001, 0)
FPSAmount.Font = Enum.Font.Code
FPSAmount.TextColor3 = Color3.fromRGB(255, 255, 255)
FPSAmount.TextScaled = true
FPSAmount.TextSize = 14.000
FPSAmount.TextWrapped = true
FPSAmount.Draggable = true
   
end);
local tab = main:CreateTab("Fake Marco")

tab:CreateLabel("Keybind V")

tab:CreateToggle("Fake Marco", function(value)
   repeat wait() until game:IsLoaded() 

getgenv().Fix = true

getgenv().TeclasWS = {
    ["tecla1"] = "M", -- speed +5
    ["tecla2"] = "N", -- speed -5
    ["tecla3"] = "V" -- toggle  
}



-- // servicios
local MININOS_DOXXEADOS = game:GetService("Players")
local AUDIOS_LOUD_DE_TRAP = game:GetService("StarterGui") or "son una mierda"

-- // objetos
local neonazi = MININOS_DOXXEADOS.LocalPlayer
local esvastica = neonazi:GetMouse()

-- // variables
local lista_de_victimas_de_drizzy = getrenv()._G
local da_hood_rblxm_REAL = getrawmetatable(game)
local CP = da_hood_rblxm_REAL.__newindex
local CP_DE_DRIZZY = da_hood_rblxm_REAL.__index
local velocidad_de_cum = 200
local es_pedofilo = true

-- // funciones para acortar codigo :]
function anunciar_atentado_terrorista(fecha_del_atentado)
    AUDIOS_LOUD_DE_TRAP:SetCore("SendNotification",{
        Title="Xlazui#2571",
        Text=fecha_del_atentado,
        Icon="rbxthumb://type=Asset&id=1332213374&w=150&h=150"
       })
end


getgenv().TECHWAREWALKSPEED_LOADED = true


wait(1.5)


anunciar_atentado_terrorista("Welcome"..TeclasWS.tecla3.."")

-- // conexión
esvastica.KeyDown:Connect(function(el_impostor)
    if el_impostor:lower() == TeclasWS.tecla1:lower() then
        velocidad_de_cum = velocidad_de_cum + 1
        anunciar_atentado_terrorista(" (speed =   "..tostring(velocidad_de_cum)..")")
    elseif el_impostor:lower() == TeclasWS.tecla2:lower() then
        velocidad_de_cum = velocidad_de_cum - 1
        anunciar_atentado_terrorista(" (speed =  "..tostring(velocidad_de_cum)..")")
    elseif el_impostor:lower() == TeclasWS.tecla3:lower() then
        if es_pedofilo then
            es_pedofilo = false
            anunciar_atentado_terrorista("speed off")
        else
            es_pedofilo = true
            anunciar_atentado_terrorista("speed on")
        end
    end
end)

-- // mi parte favorita: metametodos
setreadonly(da_hood_rblxm_REAL,false)
da_hood_rblxm_REAL.__index = newcclosure(function(BEST_ON_TOP,IS_GARBAGE)
    local esPedofilo = checkcaller()
    if IS_GARBAGE == "WalkSpeed" and not esPedofilo then
        return lista_de_victimas_de_drizzy.CurrentWS
    end
    return CP_DE_DRIZZY(BEST_ON_TOP,IS_GARBAGE)
end)
da_hood_rblxm_REAL.__newindex = newcclosure(function(kaias,ip,logger)
    local unNeonazi = checkcaller()
    if es_pedofilo then
        if ip == "WalkSpeed" and logger ~= 0 and not unNeonazi then
            return CP(kaias,ip,velocidad_de_cum)
        end
    end
    return CP(kaias,ip,logger)
end)
setreadonly(da_hood_rblxm_REAL,true)

repeat wait() until game:IsLoaded()
local Players = game:service('Players')
local Player = Players.LocalPlayer

repeat wait() until Player.Character

local userInput = game:service('UserInputService')
local runService = game:service('RunService')

local Multiplier = -0.22
local Enabled = false
local whentheflashnoiq

userInput.InputBegan:connect(function(Key)
    if Key.KeyCode == Enum.KeyCode.LeftBracket then
        Multiplier = Multiplier + 0.01
        print(Multiplier)
        wait(0.2)
        while userInput:IsKeyDown(Enum.KeyCode.LeftBracket) do
            wait()
            Multiplier = Multiplier + 0.01
            print(Multiplier)
        end
    end

    if Key.KeyCode == Enum.KeyCode.RightBracket then
        Multiplier = Multiplier - 0.01
        print(Multiplier)
        wait(0.2)
        while userInput:IsKeyDown(Enum.KeyCode.RightBracket) do
            wait()
            Multiplier = Multiplier - 0.01
            print(Multiplier)
        end
    end

    if Key.KeyCode == Enum.KeyCode.P then
        Enabled = not Enabled
        if Enabled == true then
            repeat
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.Humanoid.MoveDirection * Multiplier
                game:GetService("RunService").Stepped:waitn()
            until Enabled == true
        end
    end
end)

if Fix == true then
    loadstring(game:HttpGet("https://raw.githubusercontent.com/youtubetutorials123/helo/main/123"))()
end
end);
local tab = main:CreateTab("Animation (FE)")

tab:CreateLabel("Made By f2r3gc#1134")

tab:CreateToggle("Toggle", function(value)
   while true do
local Animate = game.Players.LocalPlayer.Character.Animate
Animate.walk.WalkAnim.AnimationId = "http://www.roblox.com/asset/?id=616168032"
Animate.run.RunAnim.AnimationId = "http://www.roblox.com/asset/?id=616163682"
game.Players.LocalPlayer.Character.Humanoid.Jump = false
wait(1)
end
end);
local tab = main:CreateTab("Anti Lock")

tab:CreateLabel("Only execute 1 time")

tab:CreateToggle("Toggle", function(value)
loadstring(game:HttpGet("https://pastebin.com/raw/STvUC3V3"))()
end);
local tab = main:CreateTab("Credit")

tab:CreateLabel("Esea2, YoltW, Nonox, Mathi")

tab:CreateToggle("NVTH", function(value)
   
end);
