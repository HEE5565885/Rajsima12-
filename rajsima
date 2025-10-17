-- 🌍 Warp + Noclip + GUI ย่อ/ขยาย + ขยับได้ (Mobile Friendly)
local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local hrp = char:WaitForChild("HumanoidRootPart")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local UIS = game:GetService("UserInputService")

-- 📍 ตำแหน่งวาร์ป (แก้ค่าได้)
local targetPos = Vector3.new(-312.8, 19.8, 83.2)
local warpSpeed = 100 -- ยิ่งมากยิ่งเร็ว

-- 💫 ระบบ Noclip
local NoclipConnection
local NoclipEnabled = false
local function NoclipOn()
	if NoclipConnection then NoclipConnection:Disconnect() end
	NoclipEnabled = true
	NoclipConnection = RunService.Stepped:Connect(function()
		if NoclipEnabled and player.Character then
			for _, v in pairs(player.Character:GetDescendants()) do
				if v:IsA("BasePart") and v.CanCollide then
					v.CanCollide = false
				end
			end
		end
	end)
end
local function NoclipOff()
	NoclipEnabled = false
	if NoclipConnection then
		NoclipConnection:Disconnect()
		NoclipConnection = nil
	end
end

-- 🚀 ระบบวาร์ป
local function WarpToTarget()
	local distance = (hrp.Position - targetPos).Magnitude
	local time = distance / warpSpeed
	local tween = TweenService:Create(
		hrp,
		TweenInfo.new(time, Enum.EasingStyle.Linear),
		{CFrame = CFrame.new(targetPos)}
	)
	tween:Play()
end

-- 🎛️ GUI หลัก
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
local Frame = Instance.new("Frame")
local WarpButton = Instance.new("TextButton")
local NoclipButton = Instance.new("TextButton")
local ToggleButton = Instance.new("TextButton")
local UICorner = Instance.new("UICorner")

-- 🧩 Frame หลัก
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 180, 0, 100)
Frame.Position = UDim2.new(0.75, 0, 0.1, 0)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.BackgroundTransparency = 0.2
Frame.Active = true
Frame.Draggable = true
UICorner.Parent = Frame

-- 🧭 ปุ่ม Warp
WarpButton.Parent = Frame
WarpButton.Size = UDim2.new(0.9, 0, 0.4, 0)
WarpButton.Position = UDim2.new(0.05, 0, 0.1, 0)
WarpButton.Text = "🚀 Warp"
WarpButton.BackgroundColor3 = Color3.fromRGB(60, 180, 75)
WarpButton.TextColor3 = Color3.fromRGB(255, 255, 255)
WarpButton.Font = Enum.Font.SourceSansBold
WarpButton.TextScaled = true
UICorner:Clone().Parent = WarpButton

-- 🧱 ปุ่ม Noclip
NoclipButton.Parent = Frame
NoclipButton.Size = UDim2.new(0.9, 0, 0.4, 0)
NoclipButton.Position = UDim2.new(0.05, 0, 0.55, 0)
NoclipButton.Text = "🧱 Noclip: OFF"
NoclipButton.BackgroundColor3 = Color3.fromRGB(180, 60, 60)
NoclipButton.TextColor3 = Color3.fromRGB(255, 255, 255)
NoclipButton.Font = Enum.Font.SourceSansBold
NoclipButton.TextScaled = true
UICorner:Clone().Parent = NoclipButton

-- 🪄 ปุ่มย่อ/ขยาย GUI
ToggleButton.Parent = ScreenGui
ToggleButton.Size = UDim2.new(0, 60, 0, 30)
ToggleButton.Position = UDim2.new(0.75, 0, 0.05, 0)
ToggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Text = "📁 GUI"
ToggleButton.Font = Enum.Font.SourceSansBold
ToggleButton.TextScaled = true
ToggleButton.Active = true
ToggleButton.Draggable = true
UICorner:Clone().Parent = ToggleButton

-- ⚙️ ปุ่มทำงาน
WarpButton.MouseButton1Click:Connect(WarpToTarget)

NoclipButton.MouseButton1Click:Connect(function()
	if NoclipEnabled then
		NoclipOff()
		NoclipButton.Text = "🧱 Noclip: OFF"
		NoclipButton.BackgroundColor3 = Color3.fromRGB(180, 60, 60)
	else
		NoclipOn()
		NoclipButton.Text = "🧱 Noclip: ON"
		NoclipButton.BackgroundColor3 = Color3.fromRGB(60, 180, 75)
	end
end)

-- 📂 ซ่อน/แสดง GUI หลัก
local guiVisible = true
ToggleButton.MouseButton1Click:Connect(function()
	guiVisible = not guiVisible
	Frame.Visible = guiVisible
	if guiVisible then
		ToggleButton.Text = "📁 Hide"
	else
		ToggleButton.Text = "📂 Show"
	end
end)
