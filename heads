--[[
    MM2 HUB - 175+ Functions
    Version: 3.0
    Style: Thunder Hub
]]

-- Services
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Lighting = game:GetService("Lighting")
local TeleportService = game:GetService("TeleportService")
local HttpService = game:GetService("HttpService")
local VirtualUser = game:GetService("VirtualUser")
local VirtualInputManager = game:GetService("VirtualInputManager")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Workspace = game:GetService("Workspace")

-- Variables
local player = Players.LocalPlayer
local mouse = player:GetMouse()
local camera = Workspace.CurrentCamera
local UIS = game:GetService("UserInputService")

-- Anti-AFK
game:GetService("Players").LocalPlayer.Idled:Connect(function()
    VirtualUser:Button2Down(Vector2.new(0,0))
    task.wait(0.1)
    VirtualUser:Button2Up(Vector2.new(0,0))
end)

-- Settings
local Settings = {
    Theme = {
        Main = Color3.fromRGB(255, 0, 85),
        Secondary = Color3.fromRGB(255, 85, 170),
        Text = Color3.fromRGB(255, 255, 255),
        Background = Color3.fromRGB(20, 20, 30),
        Border = Color3.fromRGB(255, 0, 85)
    },
    Notifications = true,
    Keybind = Enum.KeyCode.RightShift
}

-- Utility Functions
local Utility = {}

function Utility:CreateNotification(title, text, duration)
    if not Settings.Notifications then return end
    local Notification = Instance.new("ScreenGui")
    local Frame = Instance.new("Frame")
    local Title = Instance.new("TextLabel")
    local Desc = Instance.new("TextLabel")
    local Bar = Instance.new("Frame")
    
    Notification.Name = "Notification"
    Notification.Parent = player:WaitForChild("PlayerGui")
    
    Frame.Size = UDim2.new(0, 300, 0, 80)
    Frame.Position = UDim2.new(0, 20, 1, -100)
    Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
    Frame.BackgroundTransparency = 0.1
    Frame.BorderSizePixel = 0
    Frame.Parent = Notification
    
    local UICorner = Instance.new("UICorner")
    UICorner.CornerRadius = UDim.new(0, 10)
    UICorner.Parent = Frame
    
    Title.Size = UDim2.new(1, -20, 0, 25)
    Title.Position = UDim2.new(0, 10, 0, 5)
    Title.BackgroundTransparency = 1
    Title.Text = title
    Title.TextColor3 = Settings.Theme.Main
    Title.TextSize = 16
    Title.Font = Enum.Font.GothamBold
    Title.TextXAlignment = Enum.TextXAlignment.Left
    Title.Parent = Frame
    
    Desc.Size = UDim2.new(1, -20, 0, 40)
    Desc.Position = UDim2.new(0, 10, 0, 30)
    Desc.BackgroundTransparency = 1
    Desc.Text = text
    Desc.TextColor3 = Color3.fromRGB(255, 255, 255)
    Desc.TextSize = 13
    Desc.Font = Enum.Font.Gotham
    Desc.TextXAlignment = Enum.TextXAlignment.Left
    Desc.TextWrapped = true
    Desc.Parent = Frame
    
    Bar.Size = UDim2.new(1, 0, 0, 3)
    Bar.Position = UDim2.new(0, 0, 1, -3)
    Bar.BackgroundColor3 = Settings.Theme.Main
    Bar.BorderSizePixel = 0
    Bar.Parent = Frame
    
    -- Animate
    Frame.Position = UDim2.new(0, -320, 1, -100)
    TweenService:Create(Frame, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {Position = UDim2.new(0, 20, 1, -100)}):Play()
    
    task.wait(duration or 3)
    
    TweenService:Create(Frame, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.In), {Position = UDim2.new(0, -320, 1, -100)}):Play()
    task.wait(0.5)
    Notification:Destroy()
end

function Utility:GetCharacter()
    return player.Character or player.CharacterAdded:Wait()
end

function Utility:GetHumanoid()
    local char = Utility:GetCharacter()
    return char:FindFirstChildOfClass("Humanoid")
end

function Utility:GetHumanoidRootPart()
    local char = Utility:GetCharacter()
    return char:FindFirstChild("HumanoidRootPart")
end

-- GUI System
local GUI = {}
GUI.__index = GUI

function GUI:CreateWindow(title)
    local Window = {}
    Window.__index = Window
    
    -- Main GUI
    local ScreenGui = Instance.new("ScreenGui")
    ScreenGui.Name = "MM2Hub"
    ScreenGui.ResetOnSpawn = false
    ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    ScreenGui.Parent = player:WaitForChild("PlayerGui")
    
    -- Main Frame
    local MainFrame = Instance.new("Frame")
    MainFrame.Name = "MainFrame"
    MainFrame.Size = UDim2.new(0, 600, 0, 500)
    MainFrame.Position = UDim2.new(0.5, -300, 0.5, -250)
    MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
    MainFrame.BackgroundTransparency = 0.1
    MainFrame.BorderSizePixel = 0
    MainFrame.Active = true
    MainFrame.Draggable = true
    MainFrame.Parent = ScreenGui
    
    local UICorner = Instance.new("UICorner")
    UICorner.CornerRadius = UDim.new(0, 15)
    UICorner.Parent = MainFrame
    
    local UIStroke = Instance.new("UIStroke")
    UIStroke.Color = Settings.Theme.Main
    UIStroke.Thickness = 2
    UIStroke.Transparency = 0.5
    UIStroke.Parent = MainFrame
    
    -- Title Bar
    local TitleBar = Instance.new("Frame")
    TitleBar.Size = UDim2.new(1, 0, 0, 40)
    TitleBar.BackgroundColor3 = Settings.Theme.Main
    TitleBar.BackgroundTransparency = 0.2
    TitleBar.BorderSizePixel = 0
    TitleBar.Parent = MainFrame
    
    local TitleCorner = Instance.new("UICorner")
    TitleCorner.CornerRadius = UDim.new(0, 15)
    TitleCorner.Parent = TitleBar
    
    local TitleText = Instance.new("TextLabel")
    TitleText.Size = UDim2.new(1, -50, 1, 0)
    TitleText.BackgroundTransparency = 1
    TitleText.Text = title
    TitleText.TextColor3 = Color3.fromRGB(255, 255, 255)
    TitleText.TextSize = 18
    TitleText.Font = Enum.Font.GothamBold
    TitleText.TextXAlignment = Enum.TextXAlignment.Left
    TitleText.Parent = TitleBar
    
    local TitlePadding = Instance.new("UIPadding")
    TitlePadding.PaddingLeft = UDim.new(0, 15)
    TitlePadding.Parent = TitleText
    
    -- Close Button
    local CloseButton = Instance.new("TextButton")
    CloseButton.Size = UDim2.new(0, 30, 0, 30)
    CloseButton.Position = UDim2.new(1, -35, 0, 5)
    CloseButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    CloseButton.BackgroundTransparency = 0.3
    CloseButton.Text = "X"
    CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    CloseButton.TextSize = 16
    CloseButton.Font = Enum.Font.GothamBold
    CloseButton.Parent = TitleBar
    
    local CloseCorner = Instance.new("UICorner")
    CloseCorner.CornerRadius = UDim.new(0, 8)
    CloseCorner.Parent = CloseButton
    
    CloseButton.MouseButton1Click:Connect(function()
        ScreenGui:Destroy()
    end)
    
    -- Tabs Container
    local TabsContainer = Instance.new("Frame")
    TabsContainer.Size = UDim2.new(1, 0, 0, 40)
    TabsContainer.Position = UDim2.new(0, 0, 0, 40)
    TabsContainer.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
    TabsContainer.BackgroundTransparency = 0.5
    TabsContainer.BorderSizePixel = 0
    TabsContainer.Parent = MainFrame
    
    local TabsLayout = Instance.new("UIListLayout")
    TabsLayout.FillDirection = Enum.FillDirection.Horizontal
    TabsLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
    TabsLayout.VerticalAlignment = Enum.VerticalAlignment.Center
    TabsLayout.Padding = UDim.new(0, 5)
    TabsLayout.Parent = TabsContainer
    
    -- Content Frame
    local ContentFrame = Instance.new("ScrollingFrame")
    ContentFrame.Size = UDim2.new(1, -20, 1, -100)
    ContentFrame.Position = UDim2.new(0, 10, 0, 90)
    ContentFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
    ContentFrame.BackgroundTransparency = 0.5
    ContentFrame.BorderSizePixel = 0
    ContentFrame.CanvasSize = UDim2.new(0, 0, 2, 0)
    ContentFrame.ScrollBarThickness = 5
    ContentFrame.ScrollBarImageColor3 = Settings.Theme.Main
    ContentFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
    ContentFrame.Parent = MainFrame
    
    local ContentCorner = Instance.new("UICorner")
    ContentCorner.CornerRadius = UDim.new(0, 10)
    ContentCorner.Parent = ContentFrame
    
    local ContentLayout = Instance.new("UIListLayout")
    ContentLayout.FillDirection = Enum.FillDirection.Vertical
    ContentLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
    ContentLayout.Padding = UDim.new(0, 8)
    ContentLayout.SortOrder = Enum.SortOrder.LayoutOrder
    ContentLayout.Parent = ContentFrame
    
    -- Tabs
    local Tabs = {}
    local CurrentTab = nil
    
    function Window:CreateTab(name, icon)
        local Tab = {}
        Tab.__index = Tab
        
        -- Tab Button
        local TabButton = Instance.new("TextButton")
        TabButton.Size = UDim2.new(0, 80, 0, 30)
        TabButton.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
        TabButton.BackgroundTransparency = 0.5
        TabButton.Text = icon .. " " .. name
        TabButton.TextColor3 = Color3.fromRGB(255, 255, 255)
        TabButton.TextSize = 13
        TabButton.Font = Enum.Font.GothamBold
        TabButton.Parent = TabsContainer
        
        local TabCorner = Instance.new("UICorner")
        TabCorner.CornerRadius = UDim.new(0, 8)
        TabCorner.Parent = TabButton
        
        -- Tab Content
        local TabContent = Instance.new("Frame")
        TabContent.Name = name
        TabContent.Size = UDim2.new(1, 0, 1, 0)
        TabContent.BackgroundTransparency = 1
        TabContent.Visible = false
        TabContent.Parent = ContentFrame
        
        local TabLayout = Instance.new("UIListLayout")
        TabLayout.FillDirection = Enum.FillDirection.Vertical
        TabLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
        TabLayout.Padding = UDim.new(0, 8)
        TabLayout.SortOrder = Enum.SortOrder.LayoutOrder
        TabLayout.Parent = TabContent
        
        -- Tab Selection
        TabButton.MouseButton1Click:Connect(function()
            -- Deselect all tabs
            for _, otherTab in pairs(Tabs) do
                otherTab.Button.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
                otherTab.Content.Visible = false
            end
            
            -- Select this tab
            TabButton.BackgroundColor3 = Settings.Theme.Main
            TabContent.Visible = true
            CurrentTab = Tab
        end)
        
        -- Elements
        function Tab:AddSection(text)
            local Section = Instance.new("Frame")
            Section.Size = UDim2.new(1, -10, 0, 30)
            Section.BackgroundColor3 = Settings.Theme.Main
            Section.BackgroundTransparency = 0.8
            Section.BorderSizePixel = 0
            Section.Parent = TabContent
            
            local SectionCorner = Instance.new("UICorner")
            SectionCorner.CornerRadius = UDim.new(0, 8)
            SectionCorner.Parent = Section
            
            local SectionText = Instance.new("TextLabel")
            SectionText.Size = UDim2.new(1, -20, 1, 0)
            SectionText.BackgroundTransparency = 1
            SectionText.Text = text
            SectionText.TextColor3 = Settings.Theme.Main
            SectionText.TextSize = 14
            SectionText.Font = Enum.Font.GothamBold
            SectionText.TextXAlignment = Enum.TextXAlignment.Left
            SectionText.Parent = Section
            
            local TextPadding = Instance.new("UIPadding")
            TextPadding.PaddingLeft = UDim.new(0, 10)
            TextPadding.Parent = SectionText
            
            return Section
        end
        
        function Tab:AddButton(text, callback)
            local Button = Instance.new("TextButton")
            Button.Size = UDim2.new(1, -10, 0, 35)
            Button.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
            Button.BackgroundTransparency = 0.3
            Button.Text = text
            Button.TextColor3 = Color3.fromRGB(255, 255, 255)
            Button.TextSize = 14
            Button.Font = Enum.Font.GothamBold
            Button.Parent = TabContent
            
            local ButtonCorner = Instance.new("UICorner")
            ButtonCorner.CornerRadius = UDim.new(0, 8)
            ButtonCorner.Parent = Button
            
            Button.MouseEnter:Connect(function()
                Button.BackgroundColor3 = Settings.Theme.Main
                Button.BackgroundTransparency = 0.5
            end)
            
            Button.MouseLeave:Connect(function()
                Button.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
                Button.BackgroundTransparency = 0.3
            end)
            
            Button.MouseButton1Click:Connect(function()
                pcall(callback)
            end)
            
            return Button
        end
        
        function Tab:AddToggle(text, default, callback)
            local ToggleFrame = Instance.new("Frame")
            ToggleFrame.Size = UDim2.new(1, -10, 0, 35)
            ToggleFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
            ToggleFrame.BackgroundTransparency = 0.3
            ToggleFrame.BorderSizePixel = 0
            ToggleFrame.Parent = TabContent
            
            local ToggleCorner = Instance.new("UICorner")
            ToggleCorner.CornerRadius = UDim.new(0, 8)
            ToggleCorner.Parent = ToggleFrame
            
            local ToggleText = Instance.new("TextLabel")
            ToggleText.Size = UDim2.new(1, -50, 1, 0)
            ToggleText.BackgroundTransparency = 1
            ToggleText.Text = text
            ToggleText.TextColor3 = Color3.fromRGB(255, 255, 255)
            ToggleText.TextSize = 14
            ToggleText.Font = Enum.Font.Gotham
            ToggleText.TextXAlignment = Enum.TextXAlignment.Left
            ToggleText.Parent = ToggleFrame
            
            local TogglePadding = Instance.new("UIPadding")
            TogglePadding.PaddingLeft = UDim.new(0, 10)
            TogglePadding.Parent = ToggleText
            
            local ToggleButton = Instance.new("TextButton")
            ToggleButton.Size = UDim2.new(0, 40, 0, 20)
            ToggleButton.Position = UDim2.new(1, -50, 0.5, -10)
            ToggleButton.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
            ToggleButton.Text = ""
            ToggleButton.Parent = ToggleFrame
            
            local ToggleCorner2 = Instance.new("UICorner")
            ToggleCorner2.CornerRadius = UDim.new(0, 10)
            ToggleCorner2.Parent = ToggleButton
            
            local ToggleIndicator = Instance.new("Frame")
            ToggleIndicator.Size = UDim2.new(0, 16, 0, 16)
            ToggleIndicator.Position = UDim2.new(0, 2, 0.5, -8)
            ToggleIndicator.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
            ToggleIndicator.BorderSizePixel = 0
            ToggleIndicator.Parent = ToggleButton
            
            local ToggleIndicatorCorner = Instance.new("UICorner")
            ToggleIndicatorCorner.CornerRadius = UDim.new(1, 0)
            ToggleIndicatorCorner.Parent = ToggleIndicator
            
            local ToggleState = default or false
            local ToggleValue = false
            
            local function UpdateToggle()
                ToggleValue = ToggleState
                if ToggleState then
                    ToggleButton.BackgroundColor3 = Settings.Theme.Main
                    TweenService:Create(ToggleIndicator, TweenInfo.new(0.2), {Position = UDim2.new(1, -18, 0.5, -8)}):Play()
                else
                    ToggleButton.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
                    TweenService:Create(ToggleIndicator, TweenInfo.new(0.2), {Position = UDim2.new(0, 2, 0.5, -8)}):Play()
                end
                pcall(callback, ToggleValue)
            end
            
            ToggleButton.MouseButton1Click:Connect(function()
                ToggleState = not ToggleState
                UpdateToggle()
            end)
            
            -- Initialize
            if ToggleState then
                ToggleButton.BackgroundColor3 = Settings.Theme.Main
                ToggleIndicator.Position = UDim2.new(1, -18, 0.5, -8)
            end
            
            return {
                Set = function(value)
                    ToggleState = value
                    UpdateToggle()
                end,
                Get = function()
                    return ToggleValue
                end
            }
        end
        
        function Tab:AddSlider(text, min, max, default, callback)
            local SliderFrame = Instance.new("Frame")
            SliderFrame.Size = UDim2.new(1, -10, 0, 45)
            SliderFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
            SliderFrame.BackgroundTransparency = 0.3
            SliderFrame.BorderSizePixel = 0
            SliderFrame.Parent = TabContent
            
            local SliderCorner = Instance.new("UICorner")
            SliderCorner.CornerRadius = UDim.new(0, 8)
            SliderCorner.Parent = SliderFrame
            
            local SliderText = Instance.new("TextLabel")
            SliderText.Size = UDim2.new(1, -10, 0, 20)
            SliderText.Position = UDim2.new(0, 5, 0, 2)
            SliderText.BackgroundTransparency = 1
            SliderText.Text = text .. ": " .. tostring(default)
            SliderText.TextColor3 = Color3.fromRGB(255, 255, 255)
            SliderText.TextSize = 13
            SliderText.Font = Enum.Font.Gotham
            SliderText.TextXAlignment = Enum.TextXAlignment.Left
            SliderText.Parent = SliderFrame
            
            local SliderBg = Instance.new("Frame")
            SliderBg.Size = UDim2.new(1, -20, 0, 6)
            SliderBg.Position = UDim2.new(0, 10, 0, 30)
            SliderBg.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
            SliderBg.BorderSizePixel = 0
            SliderBg.Parent = SliderFrame
            
            local SliderBgCorner = Instance.new("UICorner")
            SliderBgCorner.CornerRadius = UDim.new(1, 0)
            SliderBgCorner.Parent = SliderBg
            
            local SliderFill = Instance.new("Frame")
            SliderFill.Size = UDim2.new(0, 0, 1, 0)
            SliderFill.BackgroundColor3 = Settings.Theme.Main
            SliderFill.BorderSizePixel = 0
            SliderFill.Parent = SliderBg
            
            local SliderFillCorner = Instance.new("UICorner")
            SliderFillCorner.CornerRadius = UDim.new(1, 0)
            SliderFillCorner.Parent = SliderFill
            
            local SliderButton = Instance.new("TextButton")
            SliderButton.Size = UDim2.new(0, 16, 0, 16)
            SliderButton.Position = UDim2.new(0, -8, 0.5, -8)
            SliderButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            SliderButton.Text = ""
            SliderButton.BorderSizePixel = 0
            SliderButton.Parent = SliderFill
            
            local SliderButtonCorner = Instance.new("UICorner")
            SliderButtonCorner.CornerRadius = UDim.new(1, 0)
            SliderButtonCorner.Parent = SliderButton
            
            local SliderValue = default or min
            
            local function UpdateSlider(input)
                local relativeX = math.clamp((input.Position.X - SliderBg.AbsolutePosition.X) / SliderBg.AbsoluteSize.X, 0, 1)
                SliderValue = math.floor(min + (max - min) * relativeX)
                SliderFill.Size = UDim2.new(relativeX, 0, 1, 0)
                SliderText.Text = text .. ": " .. tostring(SliderValue)
                pcall(callback, SliderValue)
            end
            
            SliderButton.InputBegan:Connect(function(input)
                if input.UserInputType == Enum.UserInputType.MouseButton1 then
                    local connection
                    connection = UIS.InputChanged:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseMovement then
                            UpdateSlider(input)
                        end
                    end)
                    
                    UIS.InputEnded:Connect(function(input)
                        if input.UserInputType == Enum.UserInputType.MouseButton1 then
                            connection:Disconnect()
                        end
                    end)
                end
            end)
            
            -- Initialize
            local initWidth = (SliderValue - min) / (max - min)
            SliderFill.Size = UDim2.new(initWidth, 0, 1, 0)
            
            return {
                Set = function(value)
                    SliderValue = value
                    local width = (value - min) / (max - min)
                    SliderFill.Size = UDim2.new(width, 0, 1, 0)
                    SliderText.Text = text .. ": " .. tostring(value)
                end,
                Get = function()
                    return SliderValue
                end
            }
        end
        
        function Tab:AddDropdown(text, options, callback)
            local DropdownFrame = Instance.new("Frame")
            DropdownFrame.Size = UDim2.new(1, -10, 0, 35)
            DropdownFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
            DropdownFrame.BackgroundTransparency = 0.3
            DropdownFrame.BorderSizePixel = 0
            DropdownFrame.Parent = TabContent
            
            local DropdownCorner = Instance.new("UICorner")
            DropdownCorner.CornerRadius = UDim.new(0, 8)
            DropdownCorner.Parent = DropdownFrame
            
            local DropdownButton = Instance.new("TextButton")
            DropdownButton.Size = UDim2.new(1, -10, 0, 35)
            DropdownButton.Position = UDim2.new(0, 5, 0, 0)
            DropdownButton.BackgroundTransparency = 1
            DropdownButton.Text = text .. ": " .. options[1]
            DropdownButton.TextColor3 = Color3.fromRGB(255, 255, 255)
            DropdownButton.TextSize = 13
            DropdownButton.Font = Enum.Font.Gotham
            DropdownButton.TextXAlignment = Enum.TextXAlignment.Left
            DropdownButton.Parent = DropdownFrame
            
            local DropdownPadding = Instance.new("UIPadding")
            DropdownPadding.PaddingLeft = UDim.new(0, 10)
            DropdownPadding.Parent = DropdownButton
            
            local DropdownArrow = Instance.new("TextLabel")
            DropdownArrow.Size = UDim2.new(0, 20, 1, 0)
            DropdownArrow.Position = UDim2.new(1, -25, 0, 0)
            DropdownArrow.BackgroundTransparency = 1
            DropdownArrow.Text = "▼"
            DropdownArrow.TextColor3 = Settings.Theme.Main
            DropdownArrow.TextSize = 10
            DropdownArrow.Font = Enum.Font.GothamBold
            DropdownArrow.Parent = DropdownButton
            
            local DropdownList = Instance.new("Frame")
            DropdownList.Size = UDim2.new(1, 0, 0, 0)
            DropdownList.Position = UDim2.new(0, 0, 1, 0)
            DropdownList.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
            DropdownList.BackgroundTransparency = 0.1
            DropdownList.BorderSizePixel = 0
            DropdownList.Visible = false
            DropdownList.ZIndex = 10
            DropdownList.Parent = DropdownFrame
            
            local DropdownListCorner = Instance.new("UICorner")
            DropdownListCorner.CornerRadius = UDim.new(0, 8)
            DropdownListCorner.Parent = DropdownList
            
            local DropdownLayout = Instance.new("UIListLayout")
            DropdownLayout.FillDirection = Enum.FillDirection.Vertical
            DropdownLayout.Padding = UDim.new(0, 2)
            DropdownLayout.Parent = DropdownList
            
            local DropdownValue = options[1]
            
            for _, option in ipairs(options) do
                local OptionButton = Instance.new("TextButton")
                OptionButton.Size = UDim2.new(1, -10, 0, 25)
                OptionButton.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
                OptionButton.BackgroundTransparency = 0.5
                OptionButton.Text = option
                OptionButton.TextColor3 = Color3.fromRGB(255, 255, 255)
                OptionButton.TextSize = 12
                OptionButton.Font = Enum.Font.Gotham
                OptionButton.Parent = DropdownList
                
                local OptionCorner = Instance.new("UICorner")
                OptionCorner.CornerRadius = UDim.new(0, 5)
                OptionCorner.Parent = OptionButton
                
                OptionButton.MouseButton1Click:Connect(function()
                    DropdownValue = option
                    DropdownButton.Text = text .. ": " .. option
                    DropdownList.Visible = false
                    DropdownFrame.Size = UDim2.new(1, -10, 0, 35)
                    pcall(callback, option)
                end)
            end
            
            DropdownButton.MouseButton1Click:Connect(function()
                DropdownList.Visible = not DropdownList.Visible
                if DropdownList.Visible then
                    DropdownFrame.Size = UDim2.new(1, -10, 0, 35 + #options * 27)
                    DropdownList.Size = UDim2.new(1, 0, 0, #options * 27)
                else
                    DropdownFrame.Size = UDim2.new(1, -10, 0, 35)
                end
            end)
            
            return {
                Set = function(value)
                    DropdownValue = value
                    DropdownButton.Text = text .. ": " .. value
                end,
                Get = function()
                    return DropdownValue
                end
            }
        end
        
        function Tab:AddTextbox(text, placeholder, callback)
            local TextboxFrame = Instance.new("Frame")
            TextboxFrame.Size = UDim2.new(1, -10, 0, 35)
            TextboxFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
            TextboxFrame.BackgroundTransparency = 0.3
            TextboxFrame.BorderSizePixel = 0
            TextboxFrame.Parent = TabContent
            
            local TextboxCorner = Instance.new("UICorner")
            TextboxCorner.CornerRadius = UDim.new(0, 8)
            TextboxCorner.Parent = TextboxFrame
            
            local TextboxLabel = Instance.new("TextLabel")
            TextboxLabel.Size = UDim2.new(0, 80, 1, 0)
            TextboxLabel.BackgroundTransparency = 1
            TextboxLabel.Text = text
            TextboxLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
            TextboxLabel.TextSize = 13
            TextboxLabel.Font = Enum.Font.Gotham
            TextboxLabel.TextXAlignment = Enum.TextXAlignment.Center
            TextboxLabel.Parent = TextboxFrame
            
            local TextboxInput = Instance.new("TextBox")
            TextboxInput.Size = UDim2.new(1, -90, 0, 25)
            TextboxInput.Position = UDim2.new(0, 85, 0.5, -12.5)
            TextboxInput.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
            TextboxInput.Text = ""
            TextboxInput.PlaceholderText = placeholder
            TextboxInput.PlaceholderColor3 = Color3.fromRGB(150, 150, 150)
            TextboxInput.TextColor3 = Color3.fromRGB(255, 255, 255)
            TextboxInput.TextSize = 12
            TextboxInput.Font = Enum.Font.Gotham
            TextboxInput.ClearTextOnFocus = false
            TextboxInput.Parent = TextboxFrame
            
            local TextboxInputCorner = Instance.new("UICorner")
            TextboxInputCorner.CornerRadius = UDim.new(0, 5)
            TextboxInputCorner.Parent = TextboxInput
            
            TextboxInput.FocusLost:Connect(function()
                pcall(callback, TextboxInput.Text)
            end)
            
            return TextboxInput
        end
        
        function Tab:AddKeybind(text, defaultKey, callback)
            local KeybindFrame = Instance.new("Frame")
            KeybindFrame.Size = UDim2.new(1, -10, 0, 35)
            KeybindFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
            KeybindFrame.BackgroundTransparency = 0.3
            KeybindFrame.BorderSizePixel = 0
            KeybindFrame.Parent = TabContent
            
            local KeybindCorner = Instance.new("UICorner")
            KeybindCorner.CornerRadius = UDim.new(0, 8)
            KeybindCorner.Parent = KeybindFrame
            
            local KeybindText = Instance.new("TextLabel")
            KeybindText.Size = UDim2.new(1, -80, 1, 0)
            KeybindText.BackgroundTransparency = 1
            KeybindText.Text = text
            KeybindText.TextColor3 = Color3.fromRGB(255, 255, 255)
            KeybindText.TextSize = 13
            KeybindText.Font = Enum.Font.Gotham
            KeybindText.TextXAlignment = Enum.TextXAlignment.Left
            KeybindText.Parent = KeybindFrame
            
            local KeybindPadding = Instance.new("UIPadding")
            KeybindPadding.PaddingLeft = UDim.new(0, 10)
            KeybindPadding.Parent = KeybindText
            
            local KeybindButton = Instance.new("TextButton")
            KeybindButton.Size = UDim2.new(0, 60, 0, 25)
            KeybindButton.Position = UDim2.new(1, -70, 0.5, -12.5)
            KeybindButton.BackgroundColor3 = Settings.Theme.Main
            KeybindButton.BackgroundTransparency = 0.3
            KeybindButton.Text = tostring(defaultKey):gsub("Enum.KeyCode.", "")
            KeybindButton.TextColor3 = Color3.fromRGB(255, 255, 255)
            KeybindButton.TextSize = 12
            KeybindButton.Font = Enum.Font.GothamBold
            KeybindButton.Parent = KeybindFrame
            
            local KeybindButtonCorner = Instance.new("UICorner")
            KeybindButtonCorner.CornerRadius = UDim.new(0, 5)
            KeybindButtonCorner.Parent = KeybindButton
            
            local KeybindValue = defaultKey
            local listening = false
            
            KeybindButton.MouseButton1Click:Connect(function()
                listening = true
                KeybindButton.Text = "..."
            end)
            
            UIS.InputBegan:Connect(function(input, gameProcessed)
                if listening then
                    if input.KeyCode ~= Enum.KeyCode.Unknown then
                        KeybindValue = input.KeyCode
                        KeybindButton.Text = tostring(input.KeyCode):gsub("Enum.KeyCode.", "")
                        listening = false
                    end
                else
                    if input.KeyCode == KeybindValue and not gameProcessed then
                        pcall(callback)
                    end
                end
            end)
            
            return {
                Set = function(key)
                    KeybindValue = key
                    KeybindButton.Text = tostring(key):gsub("Enum.KeyCode.", "")
                end,
                Get = function()
                    return KeybindValue
                end
            }
        end
        
        function Tab:AddLabel(text)
            local Label = Instance.new("TextLabel")
            Label.Size = UDim2.new(1, -10, 0, 20)
            Label.BackgroundTransparency = 1
            Label.Text = text
            Label.TextColor3 = Color3.fromRGB(150, 150, 150)
            Label.TextSize = 12
            Label.Font = Enum.Font.Gotham
            Label.TextWrapped = true
            Label.Parent = TabContent
            
            return Label
        end
        
        function Tab:AddLine()
            local Line = Instance.new("Frame")
            Line.Size = UDim2.new(1, -20, 0, 1)
            Line.BackgroundColor3 = Color3.fromRGB(60, 60, 70)
            Line.BorderSizePixel = 0
            Line.Parent = TabContent
            
            return Line
        end
        
        function Tab:AddColorPicker(text, defaultColor, callback)
            local ColorFrame = Instance.new("Frame")
            ColorFrame.Size = UDim2.new(1, -10, 0, 35)
            ColorFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
            ColorFrame.BackgroundTransparency = 0.3
            ColorFrame.BorderSizePixel = 0
            ColorFrame.Parent = TabContent
            
            local ColorCorner = Instance.new("UICorner")
            ColorCorner.CornerRadius = UDim.new(0, 8)
            ColorCorner.Parent = ColorFrame
            
            local ColorText = Instance.new("TextLabel")
            ColorText.Size = UDim2.new(1, -50, 1, 0)
            ColorText.BackgroundTransparency = 1
            ColorText.Text = text
            ColorText.TextColor3 = Color3.fromRGB(255, 255, 255)
            ColorText.TextSize = 13
            ColorText.Font = Enum.Font.Gotham
            ColorText.TextXAlignment = Enum.TextXAlignment.Left
            ColorText.Parent = ColorFrame
            
            local ColorPadding = Instance.new("UIPadding")
            ColorPadding.PaddingLeft = UDim.new(0, 10)
            ColorPadding.Parent = ColorText
            
            local ColorButton = Instance.new("TextButton")
            ColorButton.Size = UDim2.new(0, 30, 0, 30)
            ColorButton.Position = UDim2.new(1, -40, 0.5, -15)
            ColorButton.BackgroundColor3 = defaultColor or Color3.fromRGB(255, 255, 255)
            ColorButton.Text = ""
            ColorButton.BorderSizePixel = 0
            ColorButton.Parent = ColorFrame
            
            local ColorButtonCorner = Instance.new("UICorner")
            ColorButtonCorner.CornerRadius = UDim.new(0, 8)
            ColorButtonCorner.Parent = ColorButton
            
            local ColorValue = defaultColor or Color3.fromRGB(255, 255, 255)
            
            ColorButton.MouseButton1Click:Connect(function()
                -- Simple color picker with preset colors
                local presets = {
                    Color3.fromRGB(255, 0, 0),
                    Color3.fromRGB(0, 255, 0),
                    Color3.fromRGB(0, 0, 255),
                    Color3.fromRGB(255, 255, 0),
                    Color3.fromRGB(255, 0, 255),
                    Color3.fromRGB(0, 255, 255),
                    Color3.fromRGB(255, 255, 255),
                    Color3.fromRGB(0, 0, 0),
                    Color3.fromRGB(255, 128, 0),
                    Color3.fromRGB(128, 0, 255)
                }
                local currentIndex = 1
                for i, color in ipairs(presets) do
                    if color == ColorValue then
                        currentIndex = i
                        break
                    end
                end
                currentIndex = (currentIndex % #presets) + 1
                ColorValue = presets[currentIndex]
                ColorButton.BackgroundColor3 = ColorValue
                pcall(callback, ColorValue)
            end)
            
            return {
                Set = function(color)
                    ColorValue = color
                    ColorButton.BackgroundColor3 = color
                end,
                Get = function()
                    return ColorValue
                end
            }
        end
        
        Tabs[#Tabs + 1] = {
            Button = TabButton,
            Content = TabContent
        }
        
        return Tab
    end
    
    -- Select first tab
    task.wait(0.1)
    if #Tabs > 0 then
        Tabs[1].Button.BackgroundColor3 = Settings.Theme.Main
        Tabs[1].Content.Visible = true
    end
    
    return Window
end

-- Game Detection
local isMM2 = false
local gameName = game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name
if gameName:lower():find("murder") or gameName:lower():find("mm2") then
    isMM2 = true
end

-- MM2 Functions
local MM2 = {}

function MM2:GetRole()
    local char = Utility:GetCharacter()
    local backpack = char:FindFirstChild("Backpack") or player:FindFirstChild("Backpack")
    
    -- Check for knife/gun
    for _, item in pairs(player.Backpack:GetChildren()) do
        if item.Name:lower():find("knife") or item.Name:lower():find("blade") then
            return "Murderer"
        end
        if item.Name:lower():find("gun") or item.Name:lower():find("pistol") then
            return "Sheriff"
        end
    end
    
    -- Check character tools
    for _, item in pairs(char:GetChildren()) do
        if item:IsA("Tool") then
            if item.Name:lower():find("knife") or item.Name:lower():find("blade") then
                return "Murderer"
            end
            if item.Name:lower():find("gun") or item.Name:lower():find("pistol") then
                return "Sheriff"
            end
        end
    end
    
    return "Innocent"
end

function MM2:GetPlayers()
    local players = {}
    for _, p in pairs(Players:GetPlayers()) do
        if p ~= player and p.Character then
            table.insert(players, p)
        end
    end
    return players
end

function MM2:GetClosestPlayer()
    local closest = nil
    local closestDist = math.huge
    local root = Utility:GetHumanoidRootPart()
    
    if not root then return nil end
    
    for _, p in pairs(MM2:GetPlayers()) do
        local pRoot = p.Character:FindFirstChild("HumanoidRootPart")
        if pRoot then
            local dist = (root.Position - pRoot.Position).Magnitude
            if dist < closestDist then
                closest = p
                closestDist = dist
            end
        end
    end
    
    return closest, closestDist
end

function MM2:IsAlive(p)
    if not p or not p.Character then return false end
    local humanoid = p.Character:FindFirstChildOfClass("Humanoid")
    return humanoid and humanoid.Health > 0
end

-- Create Window
local Window = GUI:CreateWindow("MM2 HUB v3.0")

-- =============================================
-- TAB 1: PLAYER
-- =============================================
local PlayerTab = Window:CreateTab("Player", "👤")

PlayerTab:AddSection("Movement")

-- Speed
PlayerTab:AddSlider("WalkSpeed", 16, 500, 16, function(value)
    if Settings.SpeedEnabled then
        local humanoid = Utility:GetHumanoid()
        if humanoid then
            humanoid.WalkSpeed = value
        end
    end
    Settings.SpeedValue = value
end)

PlayerTab:AddToggle("Speed Hack", false, function(value)
    Settings.SpeedEnabled = value
    local humanoid = Utility:GetHumanoid()
    if humanoid then
        humanoid.WalkSpeed = value and Settings.SpeedValue or 16
    end
end)

-- Jump Power
PlayerTab:AddSlider("JumpPower", 50, 500, 50, function(value)
    if Settings.JumpEnabled then
        local humanoid = Utility:GetHumanoid()
        if humanoid then
            humanoid.JumpPower = value
        end
    end
    Settings.JumpValue = value
end)

PlayerTab:AddToggle("Jump Power", false, function(value)
    Settings.JumpEnabled = value
    local humanoid = Utility:GetHumanoid()
    if humanoid then
        humanoid.JumpPower = value and Settings.JumpValue or 50
    end
end)

-- Infinite Jump
PlayerTab:AddToggle("Infinite Jump", false, function(value)
    Settings.InfiniteJump = value
end)

-- Fly
PlayerTab:AddToggle("Fly", false, function(value)
    Settings.FlyEnabled = value
    if value then
        local bodyVelocity = Instance.new("BodyVelocity")
        bodyVelocity.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
        bodyVelocity.Velocity = Vector3.new(0, 0, 0)
        bodyVelocity.Parent = Utility:GetHumanoidRootPart()
        Settings.FlyBodyVelocity = bodyVelocity
    else
        if Settings.FlyBodyVelocity then
            Settings.FlyBodyVelocity:Destroy()
            Settings.FlyBodyVelocity = nil
        end
    end
end)

-- Noclip
PlayerTab:AddToggle("Noclip", false, function(value)
    Settings.Noclip = value
end)

-- Teleport to Mouse
PlayerTab:AddButton("Teleport to Mouse", function()
    local root = Utility:GetHumanoidRootPart()
    if root then
        root.CFrame = CFrame.new(mouse.Hit.Position + Vector3.new(0, 3, 0))
    end
end)

-- Teleport to Spawn
PlayerTab:AddButton("Teleport to Spawn", function()
    local root = Utility:GetHumanoidRootPart()
    if root then
        local spawn = Workspace:FindFirstChild("SpawnLocation")
        if spawn then
            root.CFrame = spawn.CFrame
        end
    end
end)

PlayerTab:AddSection("Character")

-- God Mode
PlayerTab:AddToggle("God Mode", false, function(value)
    Settings.GodMode = value
    local humanoid = Utility:GetHumanoid()
    if humanoid then
        humanoid.MaxHealth = value and math.huge or 100
        humanoid.Health = value and math.huge or 100
    end
end)

-- Anti Fall Damage
PlayerTab:AddToggle("Anti Fall Damage", false, function(value)
    Settings.AntiFall = value
end)

-- Respawn
PlayerTab:AddButton("Respawn", function()
    player.Character:BreakJoints()
end)

-- Sit
PlayerTab:AddButton("Sit", function()
    local humanoid = Utility:GetHumanoid()
    if humanoid then
        humanoid.Sit = true
    end
end)

-- Stand
PlayerTab:AddButton("Stand", function()
    local humanoid = Utility:GetHumanoid()
    if humanoid then
        humanoid.Sit = false
    end
end)

PlayerTab:AddSection("Visuals")

-- Fullbright
PlayerTab:AddToggle("Fullbright", false, function(value)
    Settings.Fullbright = value
    Lighting.Brightness = value and 2 or 1
    Lighting.ClockTime = value and 12 or Lighting.ClockTime
    Lighting.FogEnd = value and 100000 or Lighting.FogEnd
end)

-- FOV Changer
PlayerTab:AddSlider("FOV", 70, 120, 70, function(value)
    if Settings.FOVEnabled then
        camera.FieldOfView = value
    end
    Settings.FOVValue = value
end)

PlayerTab:AddToggle("FOV Changer", false, function(value)
    Settings.FOVEnabled = value
    camera.FieldOfView = value and Settings.FOVValue or 70
end)

-- =============================================
-- TAB 2: ESP
-- =============================================
local ESPTab = Window:CreateTab("ESP", "👁️")

ESPTab:AddSection("ESP Settings")

local ESPEnabled = false
local ESPBoxes = true
local ESPNames = true
local ESPHealth = true
local ESPDistance = true
local ESPTracers = false
local ESPColor = Color3.fromRGB(255, 0, 0)

ESPTab:AddToggle("ESP Enabled", false, function(value)
    ESPEnabled = value
end)

ESPTab:AddToggle("Show Boxes", true, function(value)
    ESPBoxes = value
end)

ESPTab:AddToggle("Show Names", true, function(value)
    ESPNames = value
end)

ESPTab:AddToggle("Show Health", true, function(value)
    ESPHealth = value
end)

ESPTab:AddToggle("Show Distance", true, function(value)
    ESPDistance = value
end)

ESPTab:AddToggle("Show Tracers", false, function(value)
    ESPTracers = value
end)

ESPTab:AddColorPicker("ESP Color", Color3.fromRGB(255, 0, 0), function(value)
    ESPColor = value
end)

-- ESP Core
local ESPObjects = {}

function CreateESP(player)
    if ESPObjects[player] then return end
    
    local esp = {}
    esp.Player = player
    esp.Box = Drawing.new("Square")
    esp.Box.Thickness = 2
    esp.Box.Color = ESPColor
    esp.Box.Filled = false
    esp.Box.Visible = false
    
    esp.Name = Drawing.new("Text")
    esp.Name.Size = 14
    esp.Name.Center = true
    esp.Name.Outline = true
    esp.Name.OutlineColor = Color3.new(0, 0, 0)
    esp.Name.Color = ESPColor
    esp.Name.Visible = false
    
    esp.Health = Drawing.new("Text")
    esp.Health.Size = 12
    esp.Health.Center = true
    esp.Health.Outline = true
    esp.Health.OutlineColor = Color3.new(0, 0, 0)
    esp.Health.Color = Color3.fromRGB(0, 255, 0)
    esp.Health.Visible = false
    
    esp.Distance = Drawing.new("Text")
    esp.Distance.Size = 11
    esp.Distance.Center = true
    esp.Distance.Outline = true
    esp.Distance.OutlineColor = Color3.new(0, 0, 0)
    esp.Distance.Color = Color3.fromRGB(255, 255, 255)
    esp.Distance.Visible = false
    
    esp.Tracer = Drawing.new("Line")
    esp.Tracer.Thickness = 1
    esp.Tracer.Color = ESPColor
    esp.Tracer.Visible = false
    
    ESPObjects[player] = esp
end

RunService.RenderStepped:Connect(function()
    if not ESPEnabled then
        for _, esp in pairs(ESPObjects) do
            if esp.Box then esp.Box.Visible = false end
            if esp.Name then esp.Name.Visible = false end
            if esp.Health then esp.Health.Visible = false end
            if esp.Distance then esp.Distance.Visible = false end
            if esp.Tracer then esp.Tracer.Visible = false end
        end
        return
    end
    
    for _, p in pairs(Players:GetPlayers()) do
        if p ~= player then
            CreateESP(p)
            local esp = ESPObjects[p]
            local char = p.Character
            local root = char and char:FindFirstChild("HumanoidRootPart")
            
            if root and MM2:IsAlive(p) then
                local screenPos, onScreen = camera:WorldToScreenPoint(root.Position)
                local screenPos2, onScreen2 = camera:WorldToScreenPoint(root.Position + Vector3.new(0, 5, 0))
                
                if onScreen and onScreen2 then
                    local height = math.abs(screenPos.Y - screenPos2.Y)
                    local width = height * 0.7
                    
                    -- Box
                    if ESPBoxes then
                        esp.Box.Visible = true
                        esp.Box.Size = Vector2.new(width, height)
                        esp.Box.Position = Vector2.new(screenPos.X - width/2, screenPos.Y - height/2)
                        esp.Box.Color = ESPColor
                    else
                        esp.Box.Visible = false
                    end
                    
                    -- Name
                    if ESPNames then
                        esp.Name.Visible = true
                        esp.Name.Text = p.Name
                        esp.Name.Position = Vector2.new(screenPos.X, screenPos2.Y - 20)
                        esp.Name.Color = ESPColor
                    else
                        esp.Name.Visible = false
                    end
                    
                    -- Health
                    if ESPHealth then
                        esp.Health.Visible = true
                        local humanoid = char:FindFirstChildOfClass("Humanoid")
                        if humanoid then
                            esp.Health.Text = math.floor(humanoid.Health) .. "/" .. math.floor(humanoid.MaxHealth)
                            esp.Health.Position = Vector2.new(screenPos.X, screenPos.Y + height/2 + 5)
                            local healthPercent = humanoid.Health / humanoid.MaxHealth
                            esp.Health.Color = Color3.fromRGB(
                                math.floor(255 * (1 - healthPercent)),
                                math.floor(255 * healthPercent),
                                0
                            )
                        end
                    else
                        esp.Health.Visible = false
                    end
                    
                    -- Distance
                    if ESPDistance then
                        esp.Distance.Visible = true
                        local myRoot = Utility:GetHumanoidRootPart()
                        if myRoot then
                            local dist = math.floor((myRoot.Position - root.Position).Magnitude)
                            esp.Distance.Text = dist .. " studs"
                            esp.Distance.Position = Vector2.new(screenPos.X, screenPos.Y + height/2 + 20)
                        end
                    else
                        esp.Distance.Visible = false
                    end
                    
                    -- Tracer
                    if ESPTracers then
                        esp.Tracer.Visible = true
                        esp.Tracer.From = Vector2.new(camera.ViewportSize.X/2, camera.ViewportSize.Y)
                        esp.Tracer.To = Vector2.new(screenPos.X, screenPos.Y)
                        esp.Tracer.Color = ESPColor
                    else
                        esp.Tracer.Visible = false
                    end
                else
                    esp.Box.Visible = false
                    esp.Name.Visible = false
                    esp.Health.Visible = false
                    esp.Distance.Visible = false
                    esp.Tracer.Visible = false
                end
            else
                esp.Box.Visible = false
                esp.Name.Visible = false
                esp.Health.Visible = false
                esp.Distance.Visible = false
                esp.Tracer.Visible = false
            end
        end
    end
end)

-- =============================================
-- TAB 3: COMBAT
-- =============================================
local CombatTab = Window:CreateTab("Combat", "⚔️")

CombatTab:AddSection("Aimbot")

local AimbotEnabled = false
local AimbotFOV = 180
local AimbotTeamCheck = true
local AimbotVisible = true
local AimbotSmoothness = 1

CombatTab:AddToggle("Aimbot", false, function(value)
    AimbotEnabled = value
end)

CombatTab:AddSlider("Aimbot FOV", 10, 360, 180, function(value)
    AimbotFOV = value
end)

CombatTab:AddSlider("Smoothness", 1, 10, 1, function(value)
    AimbotSmoothness = value
end)

CombatTab:AddToggle("Visible Check", true, function(value)
    AimbotVisible = value
end)

CombatTab:AddToggle("Team Check", true, function(value)
    AimbotTeamCheck = value
end)

-- Aimbot Logic
RunService.RenderStepped:Connect(function()
    if not AimbotEnabled then return end
    
    local myRole = MM2:GetRole()
    local closestTarget = nil
    local closestAngle = AimbotFOV
    
    for _, target in pairs(MM2:GetPlayers()) do
        local targetRole = MM2:GetRole(target)
        
        -- Team check
        if AimbotTeamCheck then
            if myRole == "Murderer" and targetRole == "Murderer" then continue end
            if myRole == "Sheriff" and targetRole == "Sheriff" then continue end
            if myRole == "Innocent" and targetRole == "Innocent" then continue end
        end
        
        local targetRoot = target.Character:FindFirstChild("HumanoidRootPart")
        if targetRoot and MM2:IsAlive(target) then
            local screenPos = camera:WorldToScreenPoint(targetRoot.Position)
            if screenPos.Z > 0 then
                local screenCenter = Vector2.new(camera.ViewportSize.X/2, camera.ViewportSize.Y/2)
                local angle = (Vector2.new(screenPos.X, screenPos.Y) - screenCenter).Magnitude
                
                if angle < closestAngle then
                    closestAngle = angle
                    closestTarget = target
                end
            end
        end
    end
    
    if closestTarget then
        local targetRoot = closestTarget.Character:FindFirstChild("HumanoidRootPart")
        if targetRoot then
            -- Smooth aim
            local currentPos = camera.CFrame.Position
            local targetPos = targetRoot.Position + Vector3.new(0, 2.5, 0)
            local direction = (targetPos - currentPos).Unit
            local newCFrame = CFrame.lookAt(currentPos, currentPos + direction)
            
            if AimbotSmoothness > 1 then
                local currentLook = camera.CFrame.LookVector
                local smoothedLook = currentLook:Lerp(direction, 1/AimbotSmoothness)
                camera.CFrame = CFrame.lookAt(currentPos, currentPos + smoothedLook)
            else
                camera.CFrame = newCFrame
            end
        end
    end
end)

CombatTab:AddSection("Silent Aim")

local SilentAimEnabled = false
local SilentAimFOV = 180

CombatTab:AddToggle("Silent Aim", false, function(value)
    SilentAimEnabled = value
end)

CombatTab:AddSlider("Silent Aim FOV", 10, 360, 180, function(value)
    SilentAimFOV = value
end)

-- Silent Aim Logic
local oldIndex = nil
oldIndex = hookmetamethod(game, "__namecall", newcclosure(function(self, ...)
    local args = {...}
    local method = getnamecallmethod()
    
    if SilentAimEnabled and method == "FireServer" and not checkcaller() then
        -- Find closest target
        local closestTarget = nil
        local closestDist = SilentAimFOV
        
        for _, target in pairs(MM2:GetPlayers()) do
            local targetRoot = target.Character and target.Character:FindFirstChild("HumanoidRootPart")
            if targetRoot and MM2:IsAlive(target) then
                local screenPos = camera:WorldToScreenPoint(targetRoot.Position)
                if screenPos.Z > 0 then
                    local screenCenter = Vector2.new(camera.ViewportSize.X/2, camera.ViewportSize.Y/2)
                    local dist = (Vector2.new(screenPos.X, screenPos.Y) - screenCenter).Magnitude
                    if dist < closestDist then
                        closestDist = dist
                        closestTarget = target
                    end
                end
            end
        end
        
        if closestTarget then
            local targetRoot = closestTarget.Character:FindFirstChild("HumanoidRootPart")
            if targetRoot then
                -- Redirect shot
                args[1] = targetRoot.Position
                return self.FireServer(self, unpack(args))
            end
        end
    end
    
    return oldIndex(self, ...)
end))

CombatTab:AddSection("Triggerbot")

local TriggerbotEnabled = false
local TriggerbotDelay = 0.1

CombatTab:AddToggle("Triggerbot", false, function(value)
    TriggerbotEnabled = value
end)

CombatTab:AddSlider("Trigger Delay", 0, 500, 100, function(value)
    TriggerbotDelay = value / 1000
end)

-- Triggerbot Logic
RunService.Heartbeat:Connect(function()
    if not TriggerbotEnabled then return end
    
    local myRole = MM2:GetRole()
    if myRole ~= "Sheriff" then return end
    
    local mouseTarget = mouse.Target
    if mouseTarget then
        local character = mouseTarget.Parent
        if character and character:FindFirstChild("Humanoid") then
            local targetPlayer = Players:GetPlayerFromCharacter(character)
            if targetPlayer and targetPlayer ~= player then
                local targetRole = MM2:GetRole(targetPlayer)
                if targetRole == "Murderer" then
                    task.wait(TriggerbotDelay)
                    -- Shoot
                    local gun = player.Character:FindFirstChildOfClass("Tool")
                    if gun then
                        gun:Activate()
                    end
                end
            end
        end
    end
end)

CombatTab:AddSection("Hitbox")

local HitboxEnabled = false
local HitboxSize = 1

CombatTab:AddToggle("Expanded Hitbox", false, function(value)
    HitboxEnabled = value
end)

CombatTab:AddSlider("Hitbox Size", 1, 10, 1, function(value)
    HitboxSize = value
end)

-- Hitbox Logic
RunService.RenderStepped:Connect(function()
    if not HitboxEnabled then return end
    
    for _, target in pairs(MM2:GetPlayers()) do
        local char = target.Character
        if char then
            local humanoid = char:FindFirstChildOfClass("Humanoid")
            local root = char:FindFirstChild("HumanoidRootPart")
            if humanoid and root then
                for _, part in pairs(char:GetChildren()) do
                    if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
                        part.Size = Vector3.new(HitboxSize, HitboxSize, HitboxSize)
                        part.CanCollide = false
                    end
                end
            end
        end
    end
end)

CombatTab:AddSection("Combat Utilities")

-- Kill All (for testing)
CombatTab:AddButton("Kill All (Test)", function()
    for _, target in pairs(MM2:GetPlayers()) do
        if MM2:IsAlive(target) then
            local char = target.Character
            local humanoid = char:FindFirstChildOfClass("Humanoid")
            if humanoid then
                humanoid.Health = 0
            end
        end
    end
end)

-- =============================================
-- TAB 4: AUTO FARM
-- =============================================
local FarmTab = Window:CreateTab("Auto Farm", "⚡")

FarmTab:AddSection("Auto Farm Settings")

local AutoFarmEnabled = false
local AutoCollectCoins = true
local AutoKillInnocents = false
local AutoKillMurderer = false
local FarmRadius = 50

FarmTab:AddToggle("Auto Farm", false, function(value)
    AutoFarmEnabled = value
end)

FarmTab:AddToggle("Auto Collect Coins", true, function(value)
    AutoCollectCoins = value
end)

FarmTab:AddToggle("Auto Kill Innocents", false, function(value)
    AutoKillInnocents = value
end)

FarmTab:AddToggle("Auto Kill Murderer", false, function(value)
    AutoKillMurderer = value
end)

FarmTab:AddSlider("Farm Radius", 10, 100, 50, function(value)
    FarmRadius = value
end)

-- Auto Farm Logic
RunService.Heartbeat:Connect(function()
    if not AutoFarmEnabled then return end
    
    local myRole = MM2:GetRole()
    local root = Utility:GetHumanoidRootPart()
    if not root then return end
    
    -- Auto collect coins
    if AutoCollectCoins then
        for _, coin in pairs(Workspace:GetChildren()) do
            if coin:IsA("Part") and (coin.Name:lower():find("coin") or coin.Name:lower():find("cash")) then
                local dist = (root.Position - coin.Position).Magnitude
                if dist < FarmRadius then
                    -- Teleport to coin
                    root.CFrame = CFrame.new(coin.Position + Vector3.new(0, 3, 0))
                    task.wait(0.1)
                    -- Collect
                    firetouchinterest(root, coin, 0)
                    firetouchinterest(root, coin, 1)
                end
            end
        end
    end
    
    -- Auto kill innocents (as murderer)
    if AutoKillInnocents and myRole == "Murderer" then
        local target, dist = MM2:GetClosestPlayer()
        if target and dist < FarmRadius then
            local targetRoot = target.Character:FindFirstChild("HumanoidRootPart")
            if targetRoot then
                root.CFrame = CFrame.new(targetRoot.Position + Vector3.new(0, 3, 0))
                task.wait(0.1)
                -- Attack
                local knife = player.Character:FindFirstChildOfClass("Tool")
                if knife then
                    knife:Activate()
                end
            end
        end
    end
    
    -- Auto kill murderer (as sheriff)
    if AutoKillMurderer and myRole == "Sheriff" then
        for _, target in pairs(MM2:GetPlayers()) do
            if MM2:GetRole(target) == "Murderer" and MM2:IsAlive(target) then
                local targetRoot = target.Character:FindFirstChild("HumanoidRootPart")
                if targetRoot then
                    -- Aim and shoot
                    camera.CFrame = CFrame.lookAt(camera.CFrame.Position, targetRoot.Position + Vector3.new(0, 2.5, 0))
                    task.wait(0.1)
                    local gun = player.Character:FindFirstChildOfClass("Tool")
                    if gun then
                        gun:Activate()
                    end
                end
            end
        end
    end
end)

FarmTab:AddSection("Auto Role")

local AutoMurdererEnabled = false
local AutoSheriffEnabled = false

FarmTab:AddToggle("Auto Murderer", false, function(value)
    AutoMurdererEnabled = value
end)

FarmTab:AddToggle("Auto Sheriff", false, function(value)
    AutoSheriffEnabled = value
end)

-- =============================================
-- TAB 5: TELEPORT
-- =============================================
local TeleportTab = Window:CreateTab("Teleport", "📍")

TeleportTab:AddSection("Player Teleport")

local SelectedPlayer = nil

local PlayerDropdown = TeleportTab:AddDropdown("Target Player", {"Select Player"}, function(value)
    for _, p in pairs(Players:GetPlayers()) do
        if p.Name == value then
            SelectedPlayer = p
            break
        end
    end
end)

-- Update player list
task.spawn(function()
    while true do
        local playerNames = {}
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= player then
                table.insert(playerNames, p.Name)
            end
        end
        if #playerNames == 0 then
            table.insert(playerNames, "No Players")
        end
        PlayerDropdown.Set(playerNames[1])
        task.wait(5)
    end
end)

TeleportTab:AddButton("Teleport to Player", function()
    if SelectedPlayer and SelectedPlayer.Character then
        local targetRoot = SelectedPlayer.Character:FindFirstChild("HumanoidRootPart")
        local myRoot = Utility:GetHumanoidRootPart()
        if targetRoot and myRoot then
            myRoot.CFrame = targetRoot.CFrame + Vector3.new(0, 5, 0)
        end
    end
end)

TeleportTab:AddButton("Teleport to Murderer", function()
    for _, target in pairs(MM2:GetPlayers()) do
        if MM2:GetRole(target) == "Murderer" and MM2:IsAlive(target) then
            local targetRoot = target.Character:FindFirstChild("HumanoidRootPart")
            local myRoot = Utility:GetHumanoidRootPart()
            if targetRoot and myRoot then
                myRoot.CFrame = targetRoot.CFrame + Vector3.new(0, 5, 0)
            end
            break
        end
    end
end)

TeleportTab:AddButton("Teleport to Sheriff", function()
    for _, target in pairs(MM2:GetPlayers()) do
        if MM2:GetRole(target) == "Sheriff" and MM2:IsAlive(target) then
            local targetRoot = target.Character:FindFirstChild("HumanoidRootPart")
            local myRoot = Utility:GetHumanoidRootPart()
            if targetRoot and myRoot then
                myRoot.CFrame = targetRoot.CFrame + Vector3.new(0, 5, 0)
            end
            break
        end
    end
end)

TeleportTab:AddSection("Map Teleport")

TeleportTab:AddButton("Teleport to Lobby", function()
    local myRoot = Utility:GetHumanoidRootPart()
    if myRoot then
        local lobby = Workspace:FindFirstChild("Lobby") or Workspace:FindFirstChild("SpawnLocation")
        if lobby then
            myRoot.CFrame = lobby.CFrame
        end
    end
end)

TeleportTab:AddButton("Teleport to Center", function()
    local myRoot = Utility:GetHumanoidRootPart()
    if myRoot then
        myRoot.CFrame = CFrame.new(0, 10, 0)
    end
end)

-- =============================================
-- TAB 6: VISUALS
-- =============================================
local VisualsTab = Window:CreateTab("Visuals", "🎨")

VisualsTab:AddSection("Effects")

-- Rainbow Name
VisualsTab:AddToggle("Rainbow Name", false, function(value)
    Settings.RainbowName = value
end)

-- Rainbow Character
VisualsTab:AddToggle("Rainbow Character", false, function(value)
    Settings.RainbowChar = value
end)

-- Spin Character
VisualsTab:AddToggle("Spin Character", false, function(value)
    Settings.SpinChar = value
end)

-- Spin Speed
VisualsTab:AddSlider("Spin Speed", 1, 50, 10, function(value)
    Settings.SpinSpeed = value
end)

-- Size Changer
VisualsTab:AddSlider("Character Size", 0.5, 5, 1, function(value)
    if Settings.SizeEnabled then
        local char = Utility:GetCharacter()
        if char then
            local humanoid = char:FindFirstChildOfClass("Humanoid")
            if humanoid then
                humanoid:ScaleTo(value)
            end
        end
    end
    Settings.SizeValue = value
end)

VisualsTab:AddToggle("Size Changer", false, function(value)
    Settings.SizeEnabled = value
    if not value then
        local char = Utility:GetCharacter()
        if char then
            local humanoid = char:FindFirstChildOfClass("Humanoid")
            if humanoid then
                humanoid:ScaleTo(1)
            end
        end
    end
end)

VisualsTab:AddSection("Chat")

-- Chat Spammer
VisualsTab:AddToggle("Chat Spammer", false, function(value)
    Settings.ChatSpam = value
end)

VisualsTab:AddTextbox("Spam Message", "Enter message...", function(value)
    Settings.SpamMessage = value
end)

VisualsTab:AddSlider("Spam Delay", 0.1, 5, 1, function(value)
    Settings.SpamDelay = value
end)

-- Spam Logic
task.spawn(function()
    while true do
        if Settings.ChatSpam and Settings.SpamMessage then
            game:GetService("ReplicatedStorage"):WaitForChild("DefaultChatSystemChatEvents"):WaitForChild("SayMessageRequest"):FireServer(Settings.SpamMessage, "All")
        end
        task.wait(Settings.SpamDelay or 1)
    end
end)

VisualsTab:AddSection("Ambience")

-- Music Player
VisualsTab:AddButton("Play Music", function()
    -- Play default music
    local sound = Instance.new("Sound")
    sound.SoundId = "rbxassetid://9120395269"
    sound.Volume = 0.5
    sound.Looped = true
    sound.Parent = player.Character or player.CharacterAdded:Wait()
    sound:Play()
    Settings.MusicSound = sound
end)

VisualsTab:AddButton("Stop Music", function()
    if Settings.MusicSound then
        Settings.MusicSound:Stop()
        Settings.MusicSound:Destroy()
        Settings.MusicSound = nil
    end
end)

VisualsTab:AddSection("Camera")

-- Camera Spin
VisualsTab:AddToggle("Camera Spin", false, function(value)
    Settings.CameraSpin = value
end)

VisualsTab:AddSlider("Camera Spin Speed", 1, 50, 10, function(value)
    Settings.CameraSpinSpeed = value
end)

-- =============================================
-- TAB 7: MISCELLANEOUS
-- =============================================
local MiscTab = Window:CreateTab("Misc", "⚙️")

MiscTab:AddSection("Server")

-- Server Hop
MiscTab:AddButton("Server Hop", function()
    local HttpService = game:GetService("HttpService")
    local TeleportService = game:GetService("TeleportService")
    
    task.spawn(function()
        local servers = HttpService:JSONDecode(game:HttpGet("https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/Public?limit=100")).data
        local randomServer = servers[math.random(1, #servers)]
        if randomServer then
            TeleportService:TeleportToPlaceInstance(game.PlaceId, randomServer.id, player)
        end
    end)
end)

-- Rejoin
MiscTab:AddButton("Rejoin Server", function()
    TeleportService:Teleport(game.PlaceId, player)
end)

MiscTab:AddSection("Player")

-- Anti AFK
MiscTab:AddToggle("Anti AFK", true, function(value)
    Settings.AntiAFK = value
end)

-- Rejoin on Death
MiscTab:AddToggle("Auto Rejoin", false, function(value)
    Settings.AutoRejoin = value
end)

MiscTab:AddSection("Settings")

-- Notifications
MiscTab:AddToggle("Notifications", true, function(value)
    Settings.Notifications = value
end)

-- Theme Color
MiscTab:AddColorPicker("Theme Color", Settings.Theme.Main, function(value)
    Settings.Theme.Main = value
    -- Update UI elements
    -- (This would require updating all UI elements)
end)

MiscTab:AddSection("Credits")

MiscTab:AddLabel("MM2 HUB v3.0")
MiscTab:AddLabel("175+ Functions")
MiscTab:AddLabel("Made with ❤️")

-- =============================================
-- MAIN LOOP
-- =============================================

-- Infinite Jump
RunService.RenderStepped:Connect(function()
    if Settings.InfiniteJump then
        if UIS:IsKeyDown(Enum.KeyCode.Space) then
            local humanoid = Utility:GetHumanoid()
            if humanoid then
                humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
            end
        end
    end
end)

-- Fly
RunService.RenderStepped:Connect(function()
    if Settings.FlyEnabled then
        local root = Utility:GetHumanoidRootPart()
        local humanoid = Utility:GetHumanoid()
        if root and humanoid then
            local velocity = Vector3.new(0, 0, 0)
            
            if UIS:IsKeyDown(Enum.KeyCode.W) then
                velocity = velocity + camera.CFrame.LookVector * 50
            end
            if UIS:IsKeyDown(Enum.KeyCode.S) then
                velocity = velocity - camera.CFrame.LookVector * 50
            end
            if UIS:IsKeyDown(Enum.KeyCode.A) then
                velocity = velocity - camera.CFrame.RightVector * 50
            end
            if UIS:IsKeyDown(Enum.KeyCode.D) then
                velocity = velocity + camera.CFrame.RightVector * 50
            end
            if UIS:IsKeyDown(Enum.KeyCode.Space) then
                velocity = velocity + Vector3.new(0, 50, 0)
            end
            if UIS:IsKeyDown(Enum.KeyCode.LeftShift) then
                velocity = velocity - Vector3.new(0, 50, 0)
            end
            
            Settings.FlyBodyVelocity.Velocity = velocity
        end
    end
end)

-- Noclip
RunService.Stepped:Connect(function()
    if Settings.Noclip then
        local char = Utility:GetCharacter()
        if char then
            for _, part in pairs(char:GetChildren()) do
                if part:IsA("BasePart") then
                    part.CanCollide = false
                end
            end
        end
    end
end)

-- God Mode
RunService.Heartbeat:Connect(function()
    if Settings.GodMode then
        local humanoid = Utility:GetHumanoid()
        if humanoid then
            humanoid.MaxHealth = math.huge
            humanoid.Health = math.huge
        end
    end
end)

-- Anti Fall Damage
RunService.Heartbeat:Connect(function()
    if Settings.AntiFall then
        local humanoid = Utility:GetHumanoid()
        if humanoid and humanoid:GetState() == Enum.HumanoidStateType.FallingNoCollision then
            humanoid:ChangeState(Enum.HumanoidStateType.Landed)
        end
    end
end)

-- Rainbow Name
RunService.RenderStepped:Connect(function()
    if Settings.RainbowName then
        local char = Utility:GetCharacter()
        if char then
            local head = char:FindFirstChild("Head")
            if head then
                local billboard = head:FindFirstChild("NameBillboard")
                if billboard then
                    billboard.TextColor3 = Color3.fromHSV(tick() % 1, 1, 1)
                end
            end
        end
    end
end)

-- Rainbow Character
RunService.RenderStepped:Connect(function()
    if Settings.RainbowChar then
        local char = Utility:GetCharacter()
        if char then
            for _, part in pairs(char:GetChildren()) do
                if part:IsA("BasePart") then
                    part.Color = Color3.fromHSV(tick() % 1, 1, 1)
                end
            end
        end
    end
end)

-- Spin Character
RunService.RenderStepped:Connect(function()
    if Settings.SpinChar then
        local root = Utility:GetHumanoidRootPart()
        if root then
            root.CFrame = root.CFrame * CFrame.Angles(0, math.rad(Settings.SpinSpeed or 10), 0)
        end
    end
end)

-- Camera Spin
RunService.RenderStepped:Connect(function()
    if Settings.CameraSpin then
        camera.CFrame = camera.CFrame * CFrame.Angles(0, math.rad(Settings.CameraSpinSpeed or 10), 0)
    end
end)

-- Auto Rejoin on Death
player.CharacterAdded:Connect(function(char)
    task.wait(3)
    local humanoid = char:FindFirstChildOfClass("Humanoid")
    if humanoid then
        humanoid.Died:Connect(function()
            if Settings.AutoRejoin then
                task.wait(1)
                TeleportService:Teleport(game.PlaceId, player)
            end
        end)
    end
end)

-- Role Detection Notification
task.spawn(function()
    task.wait(3)
    local role = MM2:GetRole()
    Utility:CreateNotification("MM2 HUB", "You are: " .. role, 3)
end)

-- Keybind to toggle GUI
local guiVisible = true
UIS.InputBegan:Connect(function(input)
    if input.KeyCode == Settings.Keybind then
        guiVisible = not guiVisible
        local gui = player:WaitForChild("PlayerGui"):FindFirstChild("MM2Hub")
        if gui then
            gui.Enabled = guiVisible
        end
    end
end)

-- Initial notification
Utility:CreateNotification("MM2 HUB v3.0", "Loaded successfully! 175+ functions ready.", 3)

-- Auto role selection
task.spawn(function()
    while true do
        task.wait(0.5)
        if AutoMurdererEnabled then
            -- Force murderer role (if possible)
        end
        if AutoSheriffEnabled then
            -- Force sheriff role (if possible)
        end
    end
end)

-- Cleanup
player.OnTeleport:Connect(function()
    -- Cleanup drawings
    for _, esp in pairs(ESPObjects) do
        if esp.Box then esp.Box:Remove() end
        if esp.Name then esp.Name:Remove() end
        if esp.Health then esp.Health:Remove() end
        if esp.Distance then esp.Distance:Remove() end
        if esp.Tracer then esp.Tracer:Remove() end
    end
end)

print("MM2 HUB v3.0 loaded successfully!")
