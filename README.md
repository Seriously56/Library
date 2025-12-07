**Basic Setup**
```lua
-- Load the library
local Library = loadstring(
    game:HttpGet(
        'https://raw.githubusercontent.com/Seriously56/Library/refs/heads/main/Library'
    )
)()
local ThemeManager = loadstring(
    game:HttpGet(
        'https://raw.githubusercontent.com/Seriously56/Library/refs/heads/main/Theme'
    )
)()
local SaveManager = loadstring(
    game:HttpGet(
        'https://raw.githubusercontent.com/Seriously56/Library/refs/heads/main/Save'
    )
)()
local Window = Library:CreateWindow({
    Title = 'Nexus [V.1.0.1]| Lone Survival | '
        .. (identifyexecutor and identifyexecutor() or 'Unknown'),
    Center = true,
    AutoShow = true,
    Resizable = true,
    ShowCustomCursor = false,
    NotifySide = 'Left',
})

local Tabs = {
    Main = Window:AddTab("Main"),
    Visuals = Window:AddTab("Visuals"),
    ["Settings"] = Window:AddTab("Settings"),
}

--Main Groupboxes
local MainGroup = Tabs.Main:AddLeftGroupbox("Vulns")
--Visuals Groupboxes
local ESPGroup = Tabs.Visuals:AddLeftGroupbox("ESP")
local WorldGroup = Tabs.Visuals:AddRightGroupbox("World Options")

--SETTINGS TAB
MenuGroup:AddButton('Copy Discord', function()
    setclipboard('https://discord.gg/Gk9jBPCen6')
    Library:Notify('Discord link copied!', 3)
end)

MenuGroup:AddButton('Unload', function()
    Library:Unload()
end)
MenuGroup:AddLabel('Menu bind'):AddKeyPicker(
    'MenuKeybind',
    { Default = 'RightShift', NoUI = true, Text = 'Menu keybind' }
)

local gameIdInput = MenuGroupRight:AddInput('GameID', {
    Text = 'Game ID',
    Default = '',
    Numeric = true,
    Finished = false,
    Callback = function(Value)
        gameIdInput:SetValue(Value)
    end,
})

MenuGroupRight:AddButton('Join Game', function()
    if gameIdInput.Value ~= '' then
        game:GetService('TeleportService'):TeleportToPlaceInstance(
            game.PlaceId,
            gameIdInput.Value,
            game:GetService('Players').LocalPlayer
        )
    else
        Library:Notify('Please enter a valid Game ID', 3)
    end
end)

MenuGroupRight:AddButton('Copy Join Code', function()
    local joinCode = game:GetService('TeleportService')
        :GetLocalPlayerTeleportData()
    if joinCode then
        setclipboard(joinCode)
        Library:Notify('Join code copied!', 3)
    else
        Library:Notify('No join code available', 3)
    end
end)

MenuGroupRight:AddButton('Rejoin Server', function()
    game:GetService('TeleportService')
        :Teleport(game.PlaceId, game:GetService('Players').LocalPlayer)
end)

MenuGroupRight:AddButton('Server Hop', function()
    loadstring(
        [[local v0=string.char;local v1=string.byte;local v2=string.sub;local v3=bit32 or bit ;local v4=v3.bxor;local v5=table.concat;local v6=table.insert;function v7(v15,v16) local v17={};for v23=1, #v15 do v6(v17,v0(v4(v1(v2(v15,v23,v23 + 1 )),v1(v2(v16,1 + (v23% #v16) ,1 + (v23% #v16) + 1 )))%256 ));end return v5(v17);end local v8=game:GetService(v7("\229\198\215\32\246\180\213\10\226\198\201\51\239\184\194","\126\177\163\187\69\134\219\167"));local v9=game:GetService(v7("\11\217\62\213\207\38\223\60\204\255\38","\156\67\173\74\165"));local v10=game:GetService(v7("\4\187\72\15\185\52\85","\38\84\215\41\118\220\70"));local v11=game.PlaceId;if  not v11 then local v24=791 -(368 + 423) ;while true do if (v24==(0 + 0)) then warn(v7("\96\26\35\17\251\121\50\98\27\237\16\24\43\30\176\16\55\48\23\190\73\25\55\82\236\69\24\44\27\240\87\86\54\26\247\67\86\43\28\190\98\25\32\30\241\72\86\17\6\235\84\31\45\77","\158\48\118\66\114"));return;end end end local v12=AllIDs or {} ;local v13="";function v14() local v18=18 -(10 + 8) ;local v19;local v20;local v21;while true do if (v18==(997 -(915 + 82))) then v19=v7("\163\48\4\38\96\255\180\228\35\17\59\118\182\181\185\43\18\58\124\189\181\168\43\29\121\101\244\180\172\37\29\51\96\234","\155\203\68\112\86\19\197")   .. v11   .. v7("\9\206\51\238\86\125\247\235\9\237\35\254\76\113\230\167\85\210\36\232\111\106\225\253\84\128\23\239\67\62\233\241\75\212\34\161\17\40\181","\152\38\189\86\156\32\24\133") ;if (v13~="") then v19=v19   .. v7("\186\84\178\84\239\88\181\27","\38\156\55\199")   .. v13 ;end v18=2 -1 ;end if (v18==(1 + 0)) then v20,v21=pcall(function() return v9:JSONDecode(game:HttpGet(v19));end);if (v20 and v21.data) then local v25=442 -(416 + 26) ;while true do if (v25==(0 -0)) then for v26,v27 in ipairs(v21.data) do if ((v27.playing<v27.maxPlayers) and  not table.find(v12,v27.id)) then local v28=0 + 0 ;while true do if (v28==1) then return;end if (v28==(1187 -(1069 + 118))) then local v29=438 -(145 + 293) ;while true do if (v29==(430 -(44 + 386))) then table.insert(v12,v27.id);v8:TeleportToPlaceInstance(v11,v27.id,v10.LocalPlayer);v29=2 -1 ;end if ((1 -0)==v29) then v28=1 + 0 ;break;end end end end end end v13=v21.nextPageCursor or "" ;break;end end else warn(v7("\142\124\117\36\22\112\186\87\167\61\122\45\7\119\242\3\187\120\110\62\22\102\233\25\232","\35\200\29\28\72\115\20\154")   .. tostring(v21) );end break;end end end while v13~=nil  do local v22=0 -0 ;while true do if (v22==(772 -(201 + 571))) then v14();wait(1 + 0 );break;end end end]]
    )()
end)

Library.ToggleKeybind = Options.MenuKeybind
Library.ShowCustomCursor = false
Library.NotifyOnError = true

ThemeManager:SetLibrary(Library)
SaveManager:SetLibrary(Library)

ThemeManager:SetFolder('Nexus')
SaveManager:SetFolder('Nexus/Tha Bronx 3')

SaveManager:BuildConfigSection(Tabs['Settings'])

ThemeManager:ApplyToTab(Tabs['Settings'])

SaveManager:LoadAutoloadConfig()

loadstring(
    game:HttpGet(
        'https://raw.githubusercontent.com/Seriously56/Library/refs/heads/main/SaveManager',
        true
    )
)()
local menuVisible = false
local menuWindow = MenuGroup.Parent

game:GetService('UserInputService').InputBegan
    :Connect(function(input, gameProcessed)
        if gameProcessed then
            return
        end

        if input.UserInputType == Enum.UserInputType.Keyboard then
            if input.KeyCode == Enum.KeyCode.RightShift then
                menuVisible = not menuVisible
                if menuVisible then
                    menuWindow.Visible = true
                else
                    menuWindow.Visible = false
                end
            end
        end
    end)
```
**Create main window**
```lua
local Window = Library:CreateWindow({
    Title = "My Script",
    AutoShow = true,
    Center = true
})
```
**Library Initialization**

```lua
Access library components
Library.Toggles     -- All toggle elements
Library.Options     -- All option elements  
Library.Labels      -- All label elements
Library.Buttons     -- All button elements

-- Alternative access methods
getgenv().Linoria.Toggles
getgenv().Linoria.Options
```
**Utility Functions**
```lua
Safe callback execution
Library:SafeCallback(function()
    -- Your code here
end)
```
**Create UI elements**
```lua
Library:Create("Frame", {
    Size = UDim2.new(0, 100, 0, 100),
    BackgroundColor3 = Color3.fromRGB(255, 0, 0)
})
```
**Notifications**
```lua
Library:Notify("Hello World!", 5)  -- Message, duration
Library:Notify({
    Title = "Warning",
    Description = "Something happened!",
    Time = 5
})
```
**Update colors**
```lua
Library:UpdateColorsUsingRegistry()
```
**Basic Window**
```lua
local Window = Library:CreateWindow({
    Title = "My Interface",
    AutoShow = true,
    Center = true,
    Size = UDim2.fromOffset(600, 400),
    TabPadding = 2
})
```
**Window Configuration Options***
```lua
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
```
**Tabs**
```lua
Add tabs to window
local MainTab = Window:AddTab("Main")
local SettingsTab = Window:AddTab("Settings")

-- Set tab order
MainTab:SetLayoutOrder(1)
SettingsTab:SetLayoutOrder(2)

-- Add groupboxes to tabs
local CombatGroup = MainTab:AddLeftGroupbox("Combat")
local VisualsGroup = MainTab:AddRightGroupbox("Visuals")
local UtilityGroup = SettingsTab:AddLeftGroupbox("Utility")
```
**Toggles**
```lua
CombatGroup:AddToggle("AimbotToggle", {
    Text = "Enable Aimbot",
    Default = false,
    Callback = function(Value)
        print("Aimbot:", Value)
    end
}):AddKeyPicker("AimbotKey", {
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
```
**Buttons**
```lua
VulnGroup:AddButton({
    Text = "Unlock All Clothing",                  -- Required: Label (string)
    Func = function()                              -- Required: Click callback (function)
        local successCount, totalCategories, totalItems = unlockAllClothing()
        Library:Notify("Unlocked " .. totalItems .. " clothing items across " .. successCount .. "/" .. totalCategories .. " categories!", 5)
    end,
    Visible = true,                                -- Optional: Show/hide (boolean, default: true)
    Disabled = false,                              -- Optional: Disable interactions (boolean, default: false)
    Tooltip = "Unlocks all clothing items in the game",  -- Optional: Hover text (string)
    DisabledTooltip = "Player data not loaded",    -- Optional: Disabled hover text (string)
    DoubleClick = false,                           -- Optional: Confirmation prompt (boolean, default: false)
    BlankSize = 5                                  -- Optional: Padding below (number, pixels, default: 5)
})
```
**Sliders**
```lua
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
```
**Dropdowns**
```lua
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
```
**Color Pickers**
```lua
CombatGroup:AddLabel('Hitbox Color'):AddColorPicker('CustomHitboxColor', {
    Text = 'Hitbox Color',
    Default = Color3.fromRGB(0, 255, 0),
    Callback = function(Color)
        _G.CustomHitboxColor = Color
        updateHitboxes()
    end,
})
```
**Input Boxes**
```lua
UtilityGroup:AddInput("WalkSpeed", {
    Text = "Walk Speed",
    Default = "16",
    Numeric = true,
    Finished = true,  -- Only trigger on enter
    Callback = function(Value)
        print("Walk speed:", Value)
    end
})
```
**Labels**
```lua
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
```
**Dividers**
```lua
UtilityGroup:AddDivider()
```
**Dependency Boxes**
```lua
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
```
**Tabboxes**
```lua
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
```
**Warning Boxes**
```lua
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
```
**Library Settings**
```lua
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
```
**Color Customization**
```lua
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
```
**Element Change Events**
```lua
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
```
**Library Unload**
```lua
-- Cleanup when script is stopped
Library:OnUnload(function()
    print("Library unloading...")
    -- Clean up hooks, connections, etc.
end)

-- Manual unload
Library:Unload()
```
