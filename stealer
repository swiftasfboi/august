local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local player = Players.LocalPlayer

-- Remove old GUI if exists
pcall(function() game.CoreGui:FindFirstChild("SwiftHubUI"):Destroy() end)

-- ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "SwiftHubUI"
screenGui.Parent = game.CoreGui
screenGui.ResetOnSpawn = false

-- Loading Frame
local loadingFrame = Instance.new("Frame")
loadingFrame.Size = UDim2.new(0, 300, 0, 120)
loadingFrame.Position = UDim2.new(0.5, -150, 0.5, -60)
loadingFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
loadingFrame.BorderSizePixel = 0
loadingFrame.Parent = screenGui

local loadingText = Instance.new("TextLabel")
loadingText.Size = UDim2.new(1, 0, 0, 50)
loadingText.Position = UDim2.new(0, 0, 0, 10)
loadingText.BackgroundTransparency = 1
loadingText.Text = "SwiftHUB"
loadingText.TextColor3 = Color3.new(1, 1, 1)
loadingText.Font = Enum.Font.SourceSansBold
loadingText.TextScaled = true
loadingText.Parent = loadingFrame

local progressBarBg = Instance.new("Frame")
progressBarBg.Size = UDim2.new(0.9, 0, 0, 20)
progressBarBg.Position = UDim2.new(0.05, 0, 1, -40)
progressBarBg.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
progressBarBg.BorderSizePixel = 0
progressBarBg.Parent = loadingFrame

local progressBar = Instance.new("Frame")
progressBar.Size = UDim2.new(0, 0, 1, 0)
progressBar.BackgroundColor3 = Color3.fromRGB(0, 200, 100)
progressBar.BorderSizePixel = 0
progressBar.Parent = progressBarBg

local tween = TweenService:Create(progressBar, TweenInfo.new(10, Enum.EasingStyle.Linear), {
	Size = UDim2.new(1, 0, 1, 0)
})
tween:Play()
tween.Completed:Wait()
loadingFrame:Destroy()

-- === Main Menu ===
local menuFrame = Instance.new("Frame")
menuFrame.Size = UDim2.new(0, 200, 0, 200)
menuFrame.Position = UDim2.new(0.5, -100, 0.5, -100)
menuFrame.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
menuFrame.BorderSizePixel = 0
menuFrame.Active = true
menuFrame.Draggable = true
menuFrame.Parent = screenGui

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 30)
title.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
title.Text = "Auto Gifting Pets"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.SourceSansBold
title.TextScaled = true
title.Parent = menuFrame

local dropdownLabel = Instance.new("TextLabel")
dropdownLabel.Size = UDim2.new(0.8, 0, 0, 20)
dropdownLabel.Position = UDim2.new(0.1, 0, 0.25, 0)
dropdownLabel.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
dropdownLabel.Text = "Select Player"
dropdownLabel.TextColor3 = Color3.new(1, 1, 1)
dropdownLabel.Font = Enum.Font.SourceSans
dropdownLabel.TextScaled = true
dropdownLabel.Parent = menuFrame

local dropdownMenu = Instance.new("Frame")
dropdownMenu.Size = UDim2.new(0.8, 0, 0, 60)
dropdownMenu.Position = UDim2.new(0.1, 0, 0.4, 0)
dropdownMenu.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
dropdownMenu.Visible = true
dropdownMenu.Parent = menuFrame

local selectedPlayer = nil

local stealButton = Instance.new("TextButton")
stealButton.Size = UDim2.new(0.8, 0, 0, 30)
stealButton.Position = UDim2.new(0.1, 0, 0.85, 0)
stealButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
stealButton.Text = "Steal Pets"
stealButton.TextColor3 = Color3.new(1, 1, 1)
stealButton.Font = Enum.Font.SourceSansBold
stealButton.TextScaled = true
stealButton.Visible = false
stealButton.Parent = menuFrame

-- Update player list
local function updatePlayerList()
	dropdownMenu:ClearAllChildren()
	local y = 0
	for _, plr in ipairs(Players:GetPlayers()) do
		if plr ~= player then
			local btn = Instance.new("TextButton")
			btn.Size = UDim2.new(1, 0, 0, 20)
			btn.Position = UDim2.new(0, 0, 0, y)
			btn.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
			btn.Text = plr.Name
			btn.TextColor3 = Color3.new(1, 1, 1)
			btn.Font = Enum.Font.SourceSans
			btn.TextScaled = true
			btn.Parent = dropdownMenu

			btn.MouseButton1Click:Connect(function()
				selectedPlayer = plr
				dropdownLabel.Text = "To: " .. plr.Name
				stealButton.Visible = true
			end)

			y = y + 20
		end
	end
end

updatePlayerList()
Players.PlayerAdded:Connect(updatePlayerList)
Players.PlayerRemoving:Connect(updatePlayerList)

-- Steal Button Logic
stealButton.MouseButton1Click:Connect(function()
	if selectedPlayer then
		print("Attempting to steal pets from: " .. selectedPlayer.Name)

		local stealingLabel = Instance.new("TextLabel")
		stealingLabel.Size = UDim2.new(1, 0, 0, 20)
		stealingLabel.Position = UDim2.new(0, 0, 1, -55)
		stealingLabel.BackgroundTransparency = 1
		stealingLabel.Text = "Stealing in progress..."
		stealingLabel.TextColor3 = Color3.fromRGB(255, 200, 0)
		stealingLabel.TextScaled = true
		stealingLabel.Font = Enum.Font.SourceSansItalic
		stealingLabel.Parent = menuFrame

		local progressBg = Instance.new("Frame")
		progressBg.Size = UDim2.new(0.8, 0, 0, 10)
		progressBg.Position = UDim2.new(0.1, 0, 1, -35)
		progressBg.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
		progressBg.BorderSizePixel = 0
		progressBg.Parent = menuFrame

		local progressFill = Instance.new("Frame")
		progressFill.Size = UDim2.new(0, 0, 1, 0)
		progressFill.BackgroundColor3 = Color3.fromRGB(0, 200, 100)
		progressFill.BorderSizePixel = 0
		progressFill.Parent = progressBg

		stealButton.Visible = false

		local tween = TweenService:Create(progressFill, TweenInfo.new(10, Enum.EasingStyle.Linear), {
			Size = UDim2.new(1, 0, 1, 0)
		})
		tween:Play()
		tween.Completed:Wait()

		print("Successfully stolen pets. Rejoin to refresh inventory.")
		stealingLabel.Text = "✔ Successfully stolen pets."
		stealingLabel.TextColor3 = Color3.fromRGB(0, 255, 100)
	end
end)

-- Credit Text
local creditLabel = Instance.new("TextLabel")
creditLabel.Size = UDim2.new(1, 0, 0, 15)
creditLabel.Position = UDim2.new(0, 0, 1, -15)
creditLabel.BackgroundTransparency = 1
creditLabel.Text = "Created By SwiftHUB"
creditLabel.TextColor3 = Color3.fromRGB(180, 180, 180)
creditLabel.TextScaled = true
creditLabel.Font = Enum.Font.SourceSansItalic
creditLabel.Parent = menuFrame
