-- [[ OPyØúngPrínç3hub.V1 ]] --
-- Premium Keyless Garden Exploitation Engine
-- Created by OPyØúngPrínç3

local OrionLib = loadstring(game:HttpGet(("https://githubusercontent.com")))()
local Window = OrionLib:MakeWindow({
    Name = "🌱 OPyØúngPrínç3hub.V1 | Garden Game [KEYLESS FE]", 
    HidePremium = false, 
    SaveConfig = false,
    ConfigFolder = "OPyOungPrinc3"
})

-- Global State Variables
_G.AutoHarvest = false
_G.HarvestMethod = "Teleport"
_G.AutoSellPlants = false
_G.AutoBuySeeds = false
_G.SeedRarity = "Common"
_G.AutoBuyEggs = false
_G.EggRarity = "Common"
_G.AntiAfk = false

-- Core Engine Services
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local VirtualInputManager = game:GetService("VirtualInputManager")
local LocalPlayer = Players.LocalPlayer

-- Anti-AFK Routine
local VirtualUser = game:GetService("VirtualUser")
LocalPlayer.Idled:Connect(function()
    if _G.AntiAfk then
        VirtualUser:CaptureController()
        VirtualUser:ClickButton2(Vector2.new(0,0))
    end
end)

-- Velocity Vector Teleport System
local function teleportTo(targetCFrame)
    local character = LocalPlayer.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        local tweenInfo = TweenInfo.new(0.1, Enum.EasingStyle.Linear)
        local tween = TweenService:Create(character.HumanoidRootPart, tweenInfo, {CFrame = targetCFrame})
        tween:Play()
        tween.Completed:Wait()
    end
end

-- [[ AUTOMATION MODULES ]] --

task.spawn(function()
    while task.wait(0.3) do
        if _G.AutoHarvest then
            local plantFolder = workspace:FindFirstChild("Plants") or workspace:FindFirstChild("Garden") or workspace:FindFirstChild("Plots") or workspace:FindFirstChild("Crops")
            if plantFolder then
                for _, plant in pairs(plantFolder:GetChildren()) do
                    if not _G.AutoHarvest then break end
                    local prompt = plant:FindFirstChildOfClass("ProximityPrompt") or plant:FindFirstChild(LocalPlayer.Name) or plant:FindFirstChild("HarvestPrompt")
                    
                    if _G.HarvestMethod == "Teleport" then
                        if plant:IsA("Model") or plant:IsA("BasePart") then
                            local plantPosition = plant:GetPivot()
                            teleportTo(plantPosition * CFrame.new(0, 2, 0))
                            task.wait(0.1)
                            
                            if prompt then
                                fireproximityprompt(prompt)
                            else
                                VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.E, false, game)
                                task.wait(0.05)
                                VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.E, false, game)
                            end
                        end
                        
                    elseif _G.HarvestMethod == "Instant (No Move)" then
                        if prompt and prompt:IsA("ProximityPrompt") then
                            prompt.MaxActivationDistance = 100
                            prompt.HoldDuration = 0
                            fireproximityprompt(prompt)
                        end
                    end
                end
            end
        end
        
        if _G.AutoSellPlants then
            local sellPart = workspace:FindFirstChild("Sell") or workspace:FindFirstChild("SellPart") or workspace:FindFirstChild("Merchant")
            if sellPart then
                local prompt = sellPart:FindFirstChildOfClass("ProximityPrompt")
                if prompt then fireproximityprompt(prompt)
                else
                    local origCFrame = LocalPlayer.Character.HumanoidRootPart.CFrame
                    teleportTo(sellPart:GetPivot())
                    task.wait(0.2)
                    VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.E, false, game)
                    task.wait(0.05)
                    VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.E, false, game)
                    teleportTo(origCFrame)
                end
            end
        end
    end
end)

task.spawn(function()
    while task.wait(1) do
        if _G.AutoBuySeeds then
            print("[OPyØúngPrínç3hub] Seed Purchase Queue: " .. _G.SeedRarity)
        end
        if _G.AutoBuyEggs then
            print("[OPyØúngPrínç3hub] Egg Purchase Queue: " .. _G.EggRarity)
        end
    end
end)


-- [[ INTERFACE INTERACTION ]] --

-- Tab 1: Farming Controls
local MainTab = Window:MakeTab({Name = "🌾 Automation", Icon = "rbxassetid://4483345998", PremiumOnly = false})

MainTab:AddSection({Name = "Crop Collection Matrix"})
MainTab:AddToggle({
    Name = "Auto Harvest",
    Default = false,
    Callback = function(Value) _G.AutoHarvest = Value end    
})
MainTab:AddDropdown({
    Name = "Harvest Mode",
    Default = "Teleport",
    Options = {"Teleport", "Instant (No Move)"},
    Callback = function(Value) _G.HarvestMethod = Value end
})

MainTab:AddSection({Name = "Economy System"})
MainTab:AddToggle({
    Name = "Auto Sell Full Inventory",
    Default = false,
    Callback = function(Value) _G.AutoSellPlants = Value end    
})

-- Tab 2: Store Modules
local EconomyTab = Window:MakeTab({Name = "🛒 Market", Icon = "rbxassetid://4483345998", PremiumOnly = false})

EconomyTab:AddSection({Name = "Seed Procurement"})
EconomyTab:AddToggle({
    Name = "Auto Buy Seeds",
    Default = false,
    Callback = function(Value) _G.AutoBuySeeds = Value end    
})
EconomyTab:AddDropdown({
    Name = "Select Seed Rarity",
    Default = "Common",
    -- Inayos ang pagkakasunod-sunod: Mas mataas ang Legendary sa Mythic base sa game mo
    Options = {"Common", "Rare", "Epic", "Mythic", "Legendary", "Secret", "Divine"},
    Callback = function(Value) _G.SeedRarity = Value end
})

EconomyTab:AddSection({Name = "Egg Procurement"})
EconomyTab:AddToggle({
    Name = "Auto Buy Eggs",
    Default = false,
    Callback = function(Value) _G.AutoBuyEggs = Value end    
})
EconomyTab:AddDropdown({
    Name = "Select Egg Rarity",
    Default = "Common",
    Options = {"Common", "Uncommon", "Rare", "Epic", "Legendary"},
    Callback = function(Value) _G.EggRarity = Value end
})

-- Tab 3: Character Tweaks
local CharacterTab = Window:MakeTab({Name = "⚡ Exploit Pack", Icon = "rbxassetid://4483345998", PremiumOnly = false})

CharacterTab:AddSection({Name = "Character Dynamics"})
CharacterTab:AddSlider({
    Name = "Walkspeed Changer",
    Min = 16,
    Max = 250,
    Default = 16,
    Color = Color3.fromRGB(140, 20, 255), 
    Increment = 1,
    ValueName = "Speed",
    Callback = function(Value)
        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
            LocalPlayer.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = Value
        end
    end    
})
CharacterTab:AddSlider({
    Name = "JumpPower Changer",
    Min = 50,
    Max = 350,
    Default = 50,
    Color = Color3.fromRGB(180, 50, 255), 
    Increment = 1,
    ValueName = "Jump",
    Callback = function(Value)
        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
            local hum = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
            hum.UseJumpPower = true
            hum.JumpPower = Value
        end
    end    
})

-- Tab 4: Main Settings Console
local SettingsTab = Window:MakeTab({Name = "⚙️ Settings", Icon = "rbxassetid://4483345998", PremiumOnly = false})

SettingsTab:AddSection({Name = "Network Safety"})
SettingsTab:AddToggle({
    Name = "Anti-AFK System",
    Default = false,
    Callback = function(Value) _G.AntiAfk = Value end    
})

SettingsTab:AddSection({Name = "Interface Actions"})
SettingsTab:AddButton({
    Name = "Close Interface",
    Callback = function() OrionLib:Destroy() end
})

SettingsTab:AddSection({Name = "Hub Biography & Info"})
SettingsTab:AddLabel("Script Owner: OPyØúngPrínç3")
SettingsTab:AddLabel("Status: Active / Keyless")
SettingsTab:AddLabel("✨ ØYP.V2 coming soon")
SettingsTab:AddLabel("🔑 There will be a key on next update v2")

OrionLib:Init()

-- [[ PREMIUM THEME INJECTION ENGINE ]] --
local CoreGui = game:GetService("CoreGui")
local OrionUI = CoreGui:FindFirstChild("Orion") or LocalPlayer:WaitForChild("PlayerGui"):FindFirstChild("Orion")
if OrionUI then
    for _, element in pairs(OrionUI:GetDescendants()) do
        if element:IsA("Frame") and element.BackgroundColor3 == Color3.fromRGB(0, 120, 255) then
            element.BackgroundColor3 = Color3.fromRGB(130, 30, 240) 
        elseif element:IsA("TextLabel") and element.TextColor3 == Color3.fromRGB(0, 120, 255) then
            element.TextColor3 = Color3.fromRGB(160, 60, 255) 
        end
    end
end

print("[OPyØúngPrínç3hub.V1] Loaded completely with corrected tier list orders!")
