local player = game:GetService("Players").LocalPlayer local playerGui = player:FindFirstChild("PlayerGui") or player:WaitForChild("PlayerGui") local TweenService = game:GetService("TweenService") local UserInputService = game:GetService("UserInputService")

local whitelist = { 7717419793,  -- Replace with actual UserIds 8359546483,  -- Replace with actual UserIds 5512878559   -- Replace with actual UserIds }

local function isWhitelisted() for _, userId in ipairs(whitelist) do if player.UserId == userId then return true end end return false end

if not isWhitelisted() then player:Kick("You are not Whitelisted bozo!") end

-- Remove old GUI if exists local oldGui = playerGui:FindFirstChild("AdvancedGui") if oldGui then oldGui:Destroy() end

local screenGui = Instance.new("ScreenGui") screenGui.Name = "AdvancedGui" screenGui.ResetOnSpawn = false screenGui.Parent = playerGui

-- === Startup Animation === local startupFrame = Instance.new("Frame") startupFrame.Size = UDim2.new(1, 0, 1, 0) startupFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0) startupFrame.BorderSizePixel = 0 startupFrame.Parent = screenGui

local logo = Instance.new("ImageLabel") logo.Size = UDim2.new(0, 150, 0, 150) logo.Position = UDim2.new(0.5, -75, 0.5, -75) logo.BackgroundTransparency = 1 logo.Image = "rbxassetid://8669816197"  -- replace this with your logo asset ID logo.ImageColor3 = Color3.fromRGB(255, 255, 255) logo.Parent = startupFrame

local titleLabel = Instance.new("TextLabel") titleLabel.Text = "Advanced GUI" titleLabel.Font = Enum.Font.GothamBlack titleLabel.TextSize = 36 titleLabel.TextColor3 = Color3.new(1,1,1) titleLabel.BackgroundTransparency = 1 titleLabel.Position = UDim2.new(0.5, -150, 0.5, 100) titleLabel.Size = UDim2.new(0, 300, 0, 50) titleLabel.TextTransparency = 1 titleLabel.Parent = startupFrame

-- Animations logo.ImageTransparency = 1 local function tween(obj, props, time) local tweenInfo = TweenInfo.new(time, Enum.EasingStyle.Quad, Enum.EasingDirection.Out) TweenService:Create(obj, tweenInfo, props):Play() end

tween(logo, {ImageTransparency = 0}, 1) task.wait(1.5) tween(titleLabel, {TextTransparency = 0}, 1)

task.wait(2)

tween(logo, {ImageTransparency = 0.8}, 1) tween(titleLabel, {TextTransparency = 0.8}, 1)

task.wait(0.8) tween(startupFrame, {BackgroundTransparency = 1}, 0.5) task.wait(0.6) startupFrame:Destroy()

-- === Main UI === local mainFrame = Instance.new("Frame") mainFrame.Size = UDim2.new(0, 500, 0, 350) mainFrame.Position = UDim2.new(0.5, -250, 0.5, -175) mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30) mainFrame.BorderSizePixel = 0 mainFrame.Parent = screenGui Instance.new("UICorner", mainFrame).CornerRadius = UDim.new(0, 12) local mainStroke = Instance.new("UIStroke", mainFrame) mainStroke.Thickness = 2 mainStroke.Color = Color3.fromRGB(60, 60, 60) mainStroke.Transparency = 0.2

-- Title Bar local titleBar = Instance.new("Frame") titleBar.Size = UDim2.new(1, 0, 0, 35) titleBar.BackgroundColor3 = Color3.fromRGB(40, 40, 40) titleBar.BorderSizePixel = 0 titleBar.Parent = mainFrame Instance.new("UICorner", titleBar).CornerRadius = UDim.new(0, 12)

local titleLabel2 = Instance.new("TextLabel") titleLabel2.Text = "Advanced GUI" titleLabel2.Font = Enum.Font.GothamSemibold titleLabel2.TextSize = 18 titleLabel2.TextColor3 = Color3.fromRGB(255, 255, 255) titleLabel2.BackgroundTransparency = 1 titleLabel2.Size = UDim2.new(1, -90, 1, 0) titleLabel2.Position = UDim2.new(0, 10, 0, 0) titleLabel2.TextXAlignment = Enum.TextXAlignment.Left titleLabel2.Parent = titleBar

-- Tab Bar local tabBar = Instance.new("Frame") tabBar.Size = UDim2.new(1, 0, 0, 40) tabBar.Position = UDim2.new(0, 0, 0, 35) tabBar.BackgroundColor3 = Color3.fromRGB(50, 50, 50) tabBar.BorderSizePixel = 0 tabBar.Parent = mainFrame

local UIListLayout = Instance.new("UIListLayout", tabBar) UIListLayout.FillDirection = Enum.FillDirection.Horizontal UIListLayout.Padding = UDim.new(0, 8)

local function createTabBtn(txt, parent) local btn = Instance.new("TextButton") btn.Size = UDim2.new(0, 120, 1, 0) btn.Text = txt btn.Font = Enum.Font.Gotham btn.TextSize = 16 btn.TextColor3 = Color3.fromRGB(255, 255, 255) btn.BackgroundColor3 = Color3.fromRGB(60, 60, 60) btn.BorderSizePixel = 0 btn.MouseEnter:Connect(function() tween(btn, {BackgroundColor3 = Color3.fromRGB(70, 70, 70)}, 0.2) end) btn.MouseLeave:Connect(function() tween(btn, {BackgroundColor3 = Color3.fromRGB(60, 60, 60)}, 0.2) end) Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 8) btn.Parent = parent return btn end

local mainTabBtn = createTabBtn("Main", tabBar) local settingsTabBtn = createTabBtn("Settings", tabBar)

local contentFrame = Instance.new("Frame") contentFrame.Size = UDim2.new(1, -20, 1, -75) contentFrame.Position = UDim2.new(0, 10, 0, 70) contentFrame.BackgroundTransparency = 1 contentFrame.Parent = mainFrame

local mainPage = Instance.new("Frame") mainPage.Size = UDim2.new(1, 0, 1, 0) mainPage.BackgroundTransparency = 1 mainPage.Parent = contentFrame

local settingsPage = Instance.new("Frame") settingsPage.Size = UDim2.new(1, 0, 1, 0) settingsPage.BackgroundTransparency = 1 settingsPage.Parent = contentFrame settingsPage.Visible = false

local function switchTab(tab) mainPage.Visible = (tab == "Main") settingsPage.Visible = (tab == "Settings") end

mainTabBtn.MouseButton1Click:Connect(function() switchTab("Main") end) settingsTabBtn.MouseButton1Click:Connect(function() switchTab("Settings") end)

-- === Main Page Content === local hitboxesFrame = Instance.new("Frame") hitboxesFrame.Size = UDim2.new(0, 440, 0, 50) hitboxesFrame.Position = UDim2.new(0, 30, 0, 200) hitboxesFrame.BackgroundColor3 = Color3.fromRGB(60, 60, 60) hitboxesFrame.BorderSizePixel = 0 hitboxesFrame.Parent = mainPage

Instance.new("UICorner", hitboxesFrame).CornerRadius = UDim.new(0, 6)

local hitboxesLabel = Instance.new("TextLabel") hitboxesLabel.Text = "Hitboxes" hitboxesLabel.Font = Enum.Font.GothamBold hitboxesLabel.TextSize = 20 hitboxesLabel.TextColor3 = Color3.fromRGB(255, 255, 255) hitboxesLabel.BackgroundTransparency = 1 hitboxesLabel.Size = UDim2.new(0, 440, 0, 50) hitboxesLabel.Position = UDim2.new(0, 0, 0, 0) hitboxesLabel.Parent = hitboxesFrame

local hitboxesToggle = Instance.new("TextButton") hitboxesToggle.Size = UDim2.new(0, 150, 0, 35) hitboxesToggle.Position = UDim2.new(1, -160, 0.5, -17) hitboxesToggle.Text = "Enable Hitboxes" hitboxesToggle.TextColor3 = Color3.fromRGB(255, 255, 255) hitboxesToggle.BackgroundColor3 = Color3.fromRGB(70, 70, 70) hitboxesToggle.BorderSizePixel = 0 Instance.new("UICorner", hitboxesToggle).CornerRadius = UDim.new(0, 8) hitboxesToggle.Parent = hitboxesFrame

hitboxesToggle.MouseEnter:Connect(function() tween(hitboxesToggle, {BackgroundColor3 = Color3.fromRGB(80, 80, 80)}, 0.2) end)

hitboxesToggle.MouseLeave:Connect(function() tween(hitboxesToggle, {BackgroundColor3 = Color3.fromRGB(70, 70, 70)}, 0.2) end)
-
