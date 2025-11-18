##Basic Setup
-- Load the library
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/Seriously56/lib/main/no"))()

-- Create main window
local Window = Library:CreateWindow({
    Title = "My Script",
    AutoShow = true,
    Center = true
})

##Library Initialization

-- Access library components
Library.Toggles     -- All toggle elements
Library.Options     -- All option elements  
Library.Labels      -- All label elements
Library.Buttons     -- All button elements

-- Alternative access methods
getgenv().Linoria.Toggles
getgenv().Linoria.Options

##Utility Functions
-- Safe callback execution
Library:SafeCallback(function()
    -- Your code here
end)

-- Create UI elements
Library:Create("Frame", {
    Size = UDim2.new(0, 100, 0, 100),
    BackgroundColor3 = Color3.fromRGB(255, 0, 0)
})

-- Notifications
Library:Notify("Hello World!", 5)  -- Message, duration
Library:Notify({
    Title = "Warning",
    Description = "Something happened!",
    Time = 5
})

-- Update colors
Library:UpdateColorsUsingRegistry()

##Basic Window
local Window = Library:CreateWindow({
    Title = "My Interface",
    AutoShow = true,
    Center = true,
    Size = UDim2.fromOffset(600, 400),
    TabPadding = 2
})

##Window Configuration Options
{
    Title = "Window Title",           -- Window title text
    AutoShow = true,                  -- Automatically show window
    Center = true,                    -- Center window on screen
    Position = UDim2.fromOffset(100, 50),  -- Custom position
    Size = UDim2.fromOffset(550, 600),     -- Window size
    TabPadding = 1,                   -- Spacing between tabs
    Resizable = true,                 -- Allow window resizing
    MenuFadeTime = 0.2,               -- Animation duration
    NotifySide = "Left"               -- Notification position
}

##Tabs
-- Add tabs to window
local MainTab = Window:AddTab("Main")
local SettingsTab = Window:AddTab("Settings")

-- Set tab order
MainTab:SetLayoutOrder(1)
SettingsTab:SetLayoutOrder(2)

-- Add groupboxes to tabs
local CombatGroup = MainTab:AddLeftGroupbox("Combat")
local VisualsGroup = MainTab:AddRightGroupbox("Visuals")
local UtilityGroup = SettingsTab:AddLeftGroupbox("Utility")

##Toggles
CombatGroup:AddToggle("AimbotToggle", {
    Text = "Enable Aimbot",
    Default = false,
    Callback = function(Value)
        print("Aimbot:", Value)
    end
})

##Buttons
UtilityGroup:AddButton("TestButton", {
    Text = "Click Me",
    Func = function()
        print("Button clicked!")
    end
})

-- Double-click confirmation button
UtilityGroup:AddButton("ResetButton", {
    Text = "Reset All",
    DoubleClick = true,
    Func = function()
        print("Reset confirmed!")
    end
})

##Sliders
CombatGroup:AddSlider("AimbotFOV", {
    Text = "Aimbot FOV",
    Default = 50,
    Min = 0,
    Max = 360,
    Rounding = 0,
    Compact = false,  -- Show label above slider
    Callback = function(Value)
        print("FOV:", Value)
    end
})

##Dropdowns
-- Basic dropdown
CombatGroup:AddDropdown("TargetSelect", {
    Text = "Target Selection",
    Default = "Closest",
    Values = {"Closest", "Farthest", "Crosshair"},
    Callback = function(Value)
        print("Target:", Value)
    end
})

-- Multi-select dropdown
CombatGroup:AddDropdown("WeaponFilter", {
    Text = "Weapon Filter",
    Default = {"Rifle", "Pistol"},
    Multi = true,
    Values = {"Rifle", "Pistol", "Shotgun", "Sniper"},
    Callback = function(Value)
        print("Weapons:", Value)
    end
})

-- Player dropdown
CombatGroup:AddDropdown("TargetPlayer", {
    Text = "Target Player", 
    SpecialType = "Player",
    AllowNull = true,
    Callback = function(Value)
        print("Selected player:", Value)
    end
})

##Color Pickers
CombatGroup:AddLabel('Hitbox Color'):AddColorPicker('CustomHitboxColor', {
    Text = 'Hitbox Color',
    Default = Color3.fromRGB(0, 255, 0),
    Callback = function(Color)
        _G.CustomHitboxColor = Color
        updateHitboxes()
    end,
})

##Keybinds
CombatGroup:AddKeyPicker("AimbotKey", {
    Text = "Aimbot Keybind",
    Default = "MouseButton2",
    Mode = "Toggle",  -- Toggle, Hold, Always
    Callback = function(Value)
        print("Keybind toggled:", Value)
    end,
    ChangedCallback = function(New)
        print("Key changed to:", New)
    end
})

##Input Boxes
UtilityGroup:AddInput("WalkSpeed", {
    Text = "Walk Speed",
    Default = "16",
    Numeric = true,
    Finished = true,  -- Only trigger on enter
    Callback = function(Value)
        print("Walk speed:", Value)
    end
})

##Labels
-- Basic label
UtilityGroup:AddLabel("Status: Ready")

-- Wrapped label  
UtilityGroup:AddLabel("This is a very long description that will wrap to multiple lines", true)

-- Label with ID for later modification
local StatusLabel = UtilityGroup:AddLabel("StatusLabel", {
    Text = "Waiting...",
    DoesWrap = false
})

-- Update label later
StatusLabel:SetText("Connected!")

##Dividers
UtilityGroup:AddDivider()

##Dependency Boxes
-- Show elements only when conditions are met
local AdvancedSettings = CombatGroup:AddDependencyBox()

AdvancedSettings:AddToggle("AdvancedAim", {
    Text = "Advanced Aim Settings",
    Default = false
})

AdvancedSettings:AddSlider("AimSmoothness", {
    Text = "Aim Smoothness", 
    Default = 0.5,
    Min = 0,
    Max = 1,
    Rounding = 2
})

-- Setup dependencies (only show when AdvancedAim is enabled)
AdvancedSettings:SetupDependencies({
    {AdvancedSettings.Toggles.AdvancedAim, true}
})

##Tabboxes
-- Create tabbed sections within groupboxes
local WeaponTabbox = CombatGroup:AddLeftTabbox("Weapons")

local RifleTab = WeaponTabbox:AddTab("Rifle")
local PistolTab = WeaponTabbox:AddTab("Pistol")

RifleTab:AddToggle("RifleAimbot", {
    Text = "Rifle Aimbot",
    Default = true
})

PistolTab:AddToggle("PistolAimbot", {
    Text = "Pistol Aimbot", 
    Default = false
})

##Warning Boxes
local MainTab = Window:AddTab("Main")

-- Add warning/notification box to tab
MainTab:UpdateWarningBox({
    Visible = true,
    Title = "Warning",
    Text = "This feature is experimental!",
    IsNormal = false  -- Red warning style
})

-- Normal info box
MainTab:UpdateWarningBox({
    Visible = true, 
    Title = "Information",
    Text = "Settings saved successfully!",
    IsNormal = true  -- Blue info style
})

##Library Settings
-- DPI scaling
Library:SetDPIScale(100)  -- 100% scale

-- Notification side
Library:SetNotifySide("Left")  -- or "Right"

-- Watermark
Library:SetWatermark("My Script v1.0")
Library:SetWatermarkVisibility(true)

-- Custom cursor
Library.ShowCustomCursor = true

-- Error notifications
Library.NotifyOnError = true

##Color Customization
-- Main colors
Library.MainColor = Color3.fromRGB(28, 28, 28)
Library.BackgroundColor = Color3.fromRGB(20, 20, 20)
Library.OutlineColor = Color3.fromRGB(50, 50, 50)
Library.FontColor = Color3.fromRGB(255, 255, 255)

-- Accent colors  
Library.AccentColor = Color3.fromRGB(0, 85, 255)
Library.AccentColorDark = Library:GetDarkerColor(Library.AccentColor)

-- Special colors
Library.RiskColor = Color3.fromRGB(255, 50, 50)  -- For risky options
Library.DisabledAccentColor = Color3.fromRGB(142, 142, 142)

##Element Change Events
local MyToggle = CombatGroup:AddToggle("MyToggle", {
    Text = "My Toggle",
    Default = false,
    Callback = function(Value)
        print("Toggle changed:", Value)
    end
})

-- Additional change handler
MyToggle:OnChanged(function(Value)
    print("Alternative change handler:", Value)
end)

##Library Unload
-- Cleanup when script is stopped
Library:OnUnload(function()
    print("Library unloading...")
    -- Clean up hooks, connections, etc.
end)

-- Manual unload
Library:Unload()
