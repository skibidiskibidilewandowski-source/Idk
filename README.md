-- UNIVERSAL UPDATE DETECTOR + GUI + AUTO-KICK
-- Works in ANY game you created

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local currentVersion = game.PlaceVersion

-- Create GUI
local gui = Instance.new("ScreenGui")
gui.Name = "UpdateGui"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 320, 0, 160)
frame.Position = UDim2.new(0.5, -160, 0.4, 0)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.BackgroundTransparency = 0.25
frame.BorderSizePixel = 0
frame.Visible = false
frame.Parent = gui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 12)
corner.Parent = frame

local text = Instance.new("TextLabel")
text.Size = UDim2.new(1, -20, 1, -20)
text.Position = UDim2.new(0, 10, 0, 10)
text.BackgroundTransparency = 1
text.TextColor3 = Color3.fromRGB(255, 255, 255)
text.TextScaled = true
text.Font = Enum.Font.GothamBold
text.Text = ""
text.Parent = frame

-- Checking loop (universal)
task.spawn(function()
	while task.wait(5) do
		if game.PlaceVersion ~= currentVersion then
			frame.Visible = true
			text.Text = "⚠️ Game Updated!\nYou will be kicked..."

			task.wait(3)
			player:Kick("⚠️ Game updated — please rejoin.")
			break
		end
	end
end)
