local Players = game:GetService("Players")
local player = Players.LocalPlayer
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")

player:WaitForChild("PlayerGui")

-- ═══════════════════════════════════════════
-- THEME
-- ═══════════════════════════════════════════
local Theme = {
	Background = Color3.fromRGB(22, 22, 22),
	Panel      = Color3.fromRGB(32, 32, 32),
	Sidebar    = Color3.fromRGB(26, 26, 26),
	Button     = Color3.fromRGB(55, 120, 220),
	ButtonHover= Color3.fromRGB(70, 140, 240),
	Danger     = Color3.fromRGB(200, 70, 70),
	Success    = Color3.fromRGB(60, 180, 90),
	Text       = Color3.fromRGB(255, 255, 255),
	SubText    = Color3.fromRGB(170, 170, 170),
	InputBg    = Color3.fromRGB(45, 45, 45),
}

-- ═══════════════════════════════════════════
-- HELPER FUNCTIONS
-- ═══════════════════════════════════════════
local function CreateCorner(parent, radius)
	local c = Instance.new("UICorner")
	c.CornerRadius = UDim.new(0, radius or 8)
	c.Parent = parent
	return c
end

local function CreateFrame(props)
	local f = Instance.new("Frame")
	f.BackgroundColor3 = props.Color or Theme.Panel
	f.BorderSizePixel = 0
	f.Size = props.Size or UDim2.new(1, 0, 1, 0)
	f.Position = props.Position or UDim2.new(0, 0, 0, 0)
	f.Visible = props.Visible ~= false
	f.Active = props.Active or false
	f.Parent = props.Parent
	if props.Corner ~= false then
		CreateCorner(f, props.CornerRadius)
	end
	return f
end

local function CreateLabel(props)
	local l = Instance.new("TextLabel")
	l.BackgroundTransparency = 1
	l.Size = props.Size or UDim2.new(1, 0, 0, 18)
	l.Position = props.Position or UDim2.new(0, 0, 0, 0)
	l.Text = props.Text or ""
	l.TextColor3 = props.Color or Theme.Text
	l.Font = props.Font or Enum.Font.Gotham
	l.TextSize = props.TextSize or 13
	l.TextXAlignment = props.Align or Enum.TextXAlignment.Left
	l.TextTruncate = props.Truncate or Enum.TextTruncate.None
	l.Parent = props.Parent
	return l
end

local function CreateButton(props)
	local b = Instance.new("TextButton")
	b.BackgroundColor3 = props.Color or Theme.Button
	b.Size = props.Size or UDim2.new(1, 0, 0, 34)
	b.Position = props.Position or UDim2.new(0, 0, 0, 0)
	b.Text = props.Text or ""
	b.TextColor3 = props.TextColor or Theme.Text
	b.Font = props.Font or Enum.Font.GothamBold
	b.TextSize = props.TextSize or 14
	b.AutoButtonColor = false
	b.ZIndex = props.ZIndex or 1
	b.Parent = props.Parent
	CreateCorner(b, props.CornerRadius or 8)

	-- hover animation
	local baseColor = props.Color or Theme.Button
	local hoverColor = props.HoverColor or Color3.new(
		math.min(baseColor.R + 0.08, 1),
		math.min(baseColor.G + 0.08, 1),
		math.min(baseColor.B + 0.08, 1)
	)
	b.MouseEnter:Connect(function()
		TweenService:Create(b, TweenInfo.new(0.15), {BackgroundColor3 = hoverColor}):Play()
	end)
	b.MouseLeave:Connect(function()
		TweenService:Create(b, TweenInfo.new(0.15), {BackgroundColor3 = baseColor}):Play()
	end)

	if props.OnClick then
		b.MouseButton1Click:Connect(props.OnClick)
	end
	return b
end

local function CreateTextBox(props)
	local t = Instance.new("TextBox")
	t.BackgroundColor3 = props.Color or Theme.InputBg
	t.Size = props.Size or UDim2.new(1, 0, 0, 30)
	t.Position = props.Position or UDim2.new(0, 0, 0, 0)
	t.Text = props.Text or ""
	t.PlaceholderText = props.Placeholder or ""
	t.PlaceholderColor3 = Color3.fromRGB(140, 140, 140)
	t.TextColor3 = Theme.Text
	t.Font = props.Font or Enum.Font.Gotham
	t.TextSize = props.TextSize or 14
	t.ClearTextOnFocus = false
	t.Parent = props.Parent
	CreateCorner(t, 6)
	return t
end

-- ═══════════════════════════════════════════
-- MAIN GUI SHELL
-- ═══════════════════════════════════════════
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "UniversalHub"
screenGui.ResetOnSpawn = false
screenGui.Parent = player.PlayerGui

local mainFrame = CreateFrame({
	Parent = screenGui,
	Color = Theme.Background,
	Size = UDim2.new(0, 460, 0, 340),
	Position = UDim2.new(0.5, -230, 0.5, -170),
	Active = true,
	CornerRadius = 12,
})
mainFrame.ClipsDescendants = true
mainFrame.BackgroundTransparency = 1 -- เริ่มโปร่งใสไว้เพื่อ fade-in

-- ===== Title Bar =====
local titleBar = CreateFrame({
	Parent = mainFrame,
	Color = Theme.Panel,
	Size = UDim2.new(1, 0, 0, 38),
	Active = true,
	CornerRadius = 12,
})

CreateLabel({
	Parent = titleBar,
	Text = "UNIVERSAL HUB",
	Size = UDim2.new(1, -90, 1, 0),
	Position = UDim2.new(0, 14, 0, 0),
	Font = Enum.Font.GothamBold,
	TextSize = 15,
})

local minimizeBtn = CreateButton({
	Parent = titleBar,
	Text = "_",
	Size = UDim2.new(0, 30, 0, 28),
	Position = UDim2.new(1, -72, 0, 5),
	Color = Color3.fromRGB(60, 60, 60),
	CornerRadius = 6,
})

local closeBtn = CreateButton({
	Parent = titleBar,
	Text = "X",
	Size = UDim2.new(0, 30, 0, 28),
	Position = UDim2.new(1, -38, 0, 5),
	Color = Theme.Danger,
	CornerRadius = 6,
})

-- ===== Body (Sidebar + Content) =====
local bodyFrame = CreateFrame({
	Parent = mainFrame,
	Color = Theme.Background,
	Size = UDim2.new(1, 0, 1, -38 - 26),
	Position = UDim2.new(0, 0, 0, 38),
	Corner = false,
})

local sidebar = CreateFrame({
	Parent = bodyFrame,
	Color = Theme.Sidebar,
	Size = UDim2.new(0, 120, 1, 0),
	Corner = false,
})

local sidebarLayout = Instance.new("UIListLayout")
sidebarLayout.Padding = UDim.new(0, 4)
sidebarLayout.SortOrder = Enum.SortOrder.LayoutOrder
sidebarLayout.Parent = sidebar

local sidebarPadding = Instance.new("UIPadding")
sidebarPadding.PaddingTop = UDim.new(0, 8)
sidebarPadding.PaddingLeft = UDim.new(0, 6)
sidebarPadding.PaddingRight = UDim.new(0, 6)
sidebarPadding.Parent = sidebar

local contentArea = CreateFrame({
	Parent = bodyFrame,
	Color = Theme.Background,
	Size = UDim2.new(1, -120, 1, 0),
	Position = UDim2.new(0, 120, 0, 0),
	Corner = false,
})
contentArea.ClipsDescendants = true

-- ===== Status Bar =====
local statusBar = CreateFrame({
	Parent = mainFrame,
	Color = Theme.Panel,
	Size = UDim2.new(1, 0, 0, 26),
	Position = UDim2.new(0, 0, 1, -26),
	Corner = false,
})

local statusLabel = CreateLabel({
	Parent = statusBar,
	Text = "Status : Ready",
	Position = UDim2.new(0, 12, 0, 0),
	Size = UDim2.new(1, -24, 1, 0),
	Color = Theme.SubText,
	TextSize = 12,
})

local function SetStatus(text)
	statusLabel.Text = "Status : " .. text
end

-- ═══════════════════════════════════════════
-- PAGE SYSTEM (Sidebar + Content สลับหน้าแบบ Slide)
-- ═══════════════════════════════════════════
local pages = {}       -- pages[name] = frame
local navButtons = {}  -- navButtons[name] = button
local currentPage = nil

local function CreatePage(name)
	local page = CreateFrame({
		Parent = contentArea,
		Color = Theme.Background,
		Size = UDim2.new(1, 0, 1, 0),
		Position = UDim2.new(0, 0, 0, 0),
		Corner = false,
		Visible = false,
	})
	pages[name] = page
	return page
end

local function SwitchPage(name)
	if currentPage == name then return end
	local newPage = pages[name]
	if not newPage then return end

	-- อัปเดตสี sidebar button
	for pname, btn in pairs(navButtons) do
		local isActive = pname == name
		TweenService:Create(btn, TweenInfo.new(0.15), {
			BackgroundColor3 = isActive and Theme.Button or Theme.Sidebar
		}):Play()
	end

	-- Slide animation: หน้าใหม่ไถลเข้าจากขวา, หน้าเก่าไถลออกทางซ้าย
	if currentPage and pages[currentPage] then
		local oldPage = pages[currentPage]
		newPage.Position = UDim2.new(1, 40, 0, 0)
		newPage.Visible = true
		newPage.BackgroundTransparency = 1

		TweenService:Create(oldPage, TweenInfo.new(0.2), {
			Position = UDim2.new(-1, -40, 0, 0)
		}):Play()

		local tw = TweenService:Create(newPage, TweenInfo.new(0.22, Enum.EasingStyle.Quad), {
			Position = UDim2.new(0, 0, 0, 0)
		})
		tw:Play()
		tw.Completed:Connect(function()
			oldPage.Visible = false
			oldPage.Position = UDim2.new(0, 0, 0, 0)
		end)
	else
		newPage.Visible = true
		newPage.Position = UDim2.new(0, 0, 0, 0)
	end

	currentPage = name
end

local function CreateNavButton(name, icon, order)
	local btn = CreateButton({
		Parent = sidebar,
		Text = icon .. "  " .. name,
		Size = UDim2.new(1, 0, 0, 34),
		Color = Theme.Sidebar,
		HoverColor = Color3.fromRGB(45, 45, 45),
		TextSize = 13,
		CornerRadius = 6,
	})
	btn.TextXAlignment = Enum.TextXAlignment.Left
	local pad = Instance.new("UIPadding")
	pad.PaddingLeft = UDim.new(0, 8)
	pad.Parent = btn
	btn.LayoutOrder = order
	btn.MouseButton1Click:Connect(function()
		SwitchPage(name)
	end)
	navButtons[name] = btn
	return btn
end

-- ═══════════════════════════════════════════
-- PAGE 1: STATS
-- ═══════════════════════════════════════════
local statsPage = CreatePage("Stats")
CreateNavButton("Stats", "📊", 1)

do
	local FIXED_VALUE = 1250
  local statNames = {"Physical", "Endurace", "Speed", "Devilfruit"}
	local statBoxes = {}

	CreateLabel({
		Parent = statsPage,
		Text = "Stats Editor",
		Position = UDim2.new(0, 14, 0, 10),
		Size = UDim2.new(1, -28, 0, 18),
		Font = Enum.Font.GothamBold,
		TextSize = 14,
	})

	for i, statName in ipairs(statNames) do
		local yPos = 36 + (i - 1) * 42

		CreateLabel({
			Parent = statsPage,
			Text = statName,
			Position = UDim2.new(0, 14, 0, yPos + 6),
			Size = UDim2.new(0, 100, 0, 28),
			Color = Theme.SubText,
		})

		local box = CreateTextBox({
			Parent = statsPage,
			Position = UDim2.new(0, 120, 0, yPos),
			Size = UDim2.new(1, -134, 0, 32),
			Placeholder = "ใส่ค่า เช่น 1000",
		})

		statBoxes[statName] = box
	end

	CreateButton({
		Parent = statsPage,
		Text = "เพิ่มค่า Stats",
		Position = UDim2.new(0, 14, 0, 36 + #statNames * 42 + 8),
		Size = UDim2.new(1, -28, 0, 36),
		Color = Theme.Button,
		OnClick = function()
			local firedCount = 0
			for statName, box in pairs(statBoxes) do
				local num = tonumber(box.Text)
				if num then
					local Event = ReplicatedStorage:FindFirstChild("Stats") and ReplicatedStorage.Stats:FindFirstChild("Up")
					if Event then
						Event:FireServer(statName, tostring(num), FIXED_VALUE)
						firedCount += 1
					end
				end
			end
			SetStatus(firedCount > 0 and ("เพิ่มค่าแล้ว " .. firedCount .. " รายการ") or "กรุณาใส่ค่าตัวเลขอย่างน้อย 1 ช่อง")
		end,
	})
end

-- ═══════════════════════════════════════════
-- PAGE 2: TELEPORT
-- ═══════════════════════════════════════════
local tpPage = CreatePage("Teleport")
CreateNavButton("Teleport", "📍", 2)

do
	local function isPlayerRelated(inst)
		if Players:GetPlayerFromCharacter(inst) then return true end
		return false
	end

	local function isExcluded(inst)
		if isPlayerRelated(inst) then return true end
		if inst:IsA("Camera") or inst:IsA("Terrain") then return true end
		if inst == screenGui then return true end
		if inst:IsA("LocalScript") or inst:IsA("Script") or inst:IsA("ModuleScript") then return true end
		return false
	end

	local function isBrowsable(inst)
		if not (inst:IsA("Folder") or inst:IsA("Model") or inst:IsA("Configuration") or inst:IsA("Workspace")) then
			return false
		end
		for _, child in ipairs(inst:GetChildren()) do
			if not isExcluded(child) and (child:IsA("Folder") or child:IsA("Model") or child:IsA("BasePart") or child:IsA("Configuration")) then
				return true
			end
		end
		return false
	end

	local function teleportTo(target)
		local character = player.Character or player.CharacterAdded:Wait()
		local hrp = character:WaitForChild("HumanoidRootPart")
		local targetPos
		if target:IsA("Model") then
			targetPos = target:GetPivot().Position
		elseif target:IsA("BasePart") then
			targetPos = target.Position
		else
			return false
		end
		hrp.CFrame = CFrame.new(targetPos + Vector3.new(0, 3, 0))
		return true
	end

	-- ส่วนพิมพ์ชื่อเอง
	CreateLabel({
		Parent = tpPage,
		Text = "ชื่อ Part / Model",
		Position = UDim2.new(0, 14, 0, 10),
		Size = UDim2.new(1, -28, 0, 16),
		Color = Theme.SubText,
	})

	local nameBox = CreateTextBox({
		Parent = tpPage,
		Position = UDim2.new(0, 14, 0, 30),
		Size = UDim2.new(1, -28, 0, 32),
		Placeholder = "ใส่ชื่อ Part หรือ Model...",
	})

	CreateButton({
		Parent = tpPage,
		Text = "Teleport",
		Position = UDim2.new(0, 14, 0, 68),
		Size = UDim2.new(1, -28, 0, 32),
		Color = Theme.Button,
		OnClick = function()
			local query = nameBox.Text
			if query == "" then
				SetStatus("กรุณาใส่ชื่อก่อน")
				return
			end
			local target = nil
			for _, inst in ipairs(workspace:GetDescendants()) do
				if inst.Name == query and (inst:IsA("Model") or inst:IsA("BasePart")) and not isExcluded(inst) then
					target = inst
					break
				end
			end
			if not target then
				SetStatus("ไม่พบ: " .. query)
				return
			end
			local success = teleportTo(target)
			SetStatus(success and ("วาปไปที่ " .. target.Name .. " แล้ว") or "ไม่สามารถวาปได้")
		end,
	})

	-- Path bar
	local pathBar = CreateFrame({
		Parent = tpPage,
		Color = Theme.InputBg,
		Position = UDim2.new(0, 14, 0, 108),
		Size = UDim2.new(1, -28, 0, 26),
		CornerRadius = 6,
	})

	local backBtn = CreateButton({
		Parent = pathBar,
		Text = "◀ Back",
		Position = UDim2.new(0, 2, 0, 2),
		Size = UDim2.new(0, 60, 1, -4),
		Color = Color3.fromRGB(60, 60, 60),
		TextSize = 11,
		CornerRadius = 5,
	})

	local pathLabel = CreateLabel({
		Parent = pathBar,
		Text = "workspace",
		Position = UDim2.new(0, 66, 0, 0),
		Size = UDim2.new(1, -110, 1, 0),
		Color = Theme.SubText,
		Truncate = Enum.TextTruncate.AtEnd,
	})

	local refreshBtn = CreateButton({
		Parent = pathBar,
		Text = "⟳",
		Position = UDim2.new(1, -38, 0, 2),
		Size = UDim2.new(0, 36, 1, -4),
		Color = Color3.fromRGB(60, 60, 60),
		CornerRadius = 5,
	})

	local listFrame = Instance.new("ScrollingFrame")
	listFrame.Size = UDim2.new(1, -28, 1, -142)
	listFrame.Position = UDim2.new(0, 14, 0, 140)
	listFrame.BackgroundColor3 = Theme.InputBg
	listFrame.BorderSizePixel = 0
	listFrame.ScrollBarThickness = 6
	listFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
	listFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
	listFrame.Parent = tpPage
	CreateCorner(listFrame, 8)

	local listLayout = Instance.new("UIListLayout")
	listLayout.Padding = UDim.new(0, 4)
	listLayout.SortOrder = Enum.SortOrder.LayoutOrder
	listLayout.Parent = listFrame

	local listPad = Instance.new("UIPadding")
	listPad.PaddingTop = UDim.new(0, 4)
	listPad.PaddingLeft = UDim.new(0, 4)
	listPad.PaddingRight = UDim.new(0, 4)
	listPad.Parent = listFrame

	local currentContainer = workspace
	local history = {}
	local refreshList

	local function getPathName(container)
		if container == workspace then return "workspace" end
		return container:GetFullName():gsub("^workspace%.", "")
	end

	local function openContainer(container)
		table.insert(history, currentContainer)
		currentContainer = container
		refreshList()
	end

	local function goBack()
		if #history > 0 then
			currentContainer = table.remove(history)
			refreshList()
		end
	end

	refreshList = function()
		pathLabel.Text = getPathName(currentContainer)

		for _, child in ipairs(listFrame:GetChildren()) do
			if child.Name == "Row" then
				child:Destroy()
			end
		end

		local order = 0
		local children = currentContainer:GetChildren()
		table.sort(children, function(a, b) return a.Name < b.Name end)

		for _, item in ipairs(children) do
			if not isExcluded(item) then
				local isFolderLike = isBrowsable(item)
				local isTeleportable = item:IsA("Model") or item:IsA("BasePart")

				if isFolderLike or isTeleportable then
					order += 1

					local row = CreateFrame({
						Parent = listFrame,
						Color = Color3.fromRGB(45, 45, 45),
						Size = UDim2.new(1, 0, 0, 30),
						CornerRadius = 6,
					})
					row.Name = "Row"
					row.LayoutOrder = order

					local mainBtn = Instance.new("TextButton")
					mainBtn.BackgroundTransparency = 1
					mainBtn.Text = ""
					mainBtn.Size = UDim2.new(1, isTeleportable and isFolderLike and -34 or 0, 1, 0)
					mainBtn.Parent = row

					local icon = isFolderLike and "📁 " or "📍 "
					CreateLabel({
						Parent = mainBtn,
						Text = icon .. item.Name .. "  [" .. item.ClassName .. "]",
						Position = UDim2.new(0, 8, 0, 0),
						Size = UDim2.new(1, -10, 1, 0),
						Truncate = Enum.TextTruncate.AtEnd,
					})

					if isFolderLike and isTeleportable then
						mainBtn.MouseButton1Click:Connect(function() openContainer(item) end)

						local tpBtn = CreateButton({
							Parent = row,
							Text = "GO",
							Position = UDim2.new(1, -32, 0, 3),
							Size = UDim2.new(0, 28, 1, -6),
							Color = Theme.Button,
							TextSize = 11,
							CornerRadius = 5,
							OnClick = function()
								local success = teleportTo(item)
								SetStatus(success and ("วาปไปที่ " .. item.Name .. " แล้ว") or "วาปไม่สำเร็จ")
							end,
						})
					elseif isFolderLike then
						mainBtn.MouseButton1Click:Connect(function() openContainer(item) end)
					else
						mainBtn.MouseButton1Click:Connect(function()
							local success = teleportTo(item)
							SetStatus(success and ("วาปไปที่ " .. item.Name .. " แล้ว") or "วาปไม่สำเร็จ")
						end)
					end
				end
			end
		end

		if order == 0 then
			local emptyLabel = CreateLabel({
				Parent = listFrame,
				Text = "ไม่มีรายการในนี้",
				Size = UDim2.new(1, 0, 0, 30),
				Color = Theme.SubText,
				Align = Enum.TextXAlignment.Center,
			})
			emptyLabel.Name = "Row"
		end
	end

	backBtn.MouseButton1Click:Connect(goBack)
	refreshBtn.MouseButton1Click:Connect(refreshList)
	refreshList()
end

-- ═══════════════════════════════════════════
-- PAGE 3: AUTO PULL
-- ═══════════════════════════════════════════
local pullPage = CreatePage("Auto Pull")
CreateNavButton("Auto Pull", "⚔", 3)

do
	CreateLabel({
		Parent = pullPage,
		Text = "Range",
		Position = UDim2.new(0, 14, 0, 10),
		Size = UDim2.new(1, -28, 0, 16),
		Color = Theme.SubText,
	})

	local distanceBox = CreateTextBox({
		Parent = pullPage,
		Position = UDim2.new(0, 14, 0, 30),
		Size = UDim2.new(0, 100, 0, 32),
		Text = "50",
		Placeholder = "ระยะ",
	})

	local showRangeBtn
	showRangeBtn = CreateButton({
		Parent = pullPage,
		Text = "☐ Show Range",
		Position = UDim2.new(0, 122, 0, 30),
		Size = UDim2.new(1, -136, 0, 32),
		Color = Color3.fromRGB(55, 55, 55),
		TextSize = 13,
	})

	local pullAllButton = CreateButton({
		Parent = pullPage,
		Text = "Start Pull All",
		Position = UDim2.new(0, 14, 0, 72),
		Size = UDim2.new(1, -28, 0, 36),
		Color = Theme.Success,
	})

	local pullRangeButton = CreateButton({
		Parent = pullPage,
		Text = "Start Pull Range",
		Position = UDim2.new(0, 14, 0, 114),
		Size = UDim2.new(1, -28, 0, 36),
		Color = Theme.Button,
	})

	distanceBox:GetPropertyChangedSignal("Text"):Connect(function()
		local filtered = distanceBox.Text:gsub("[^%d]", "")
		if filtered ~= distanceBox.Text then
			distanceBox.Text = filtered
		end
	end)

	-- ===== ตรวจสอบโมเดล Player =====
	local function isPlayerRelated(inst)
		return Players:GetPlayerFromCharacter(inst) ~= nil
	end

	local function safeGetPivotPosition(inst)
		local ok, pivot = pcall(function() return inst:GetPivot() end)
		return ok and pivot.Position or nil
	end

	-- ===== Cache มอบแบบ event-driven =====
	local cachedMobs = {}

	local function tryAddModel(model)
		if not model:IsA("Model") then return end
		if cachedMobs[model] then return end
		if isPlayerRelated(model) then return end
		local humanoid = model:FindFirstChild("Humanoid")
		if humanoid and humanoid:IsA("Humanoid") then
			cachedMobs[model] = humanoid
		end
	end

	local function removeModel(model)
		cachedMobs[model] = nil
	end

	task.spawn(function()
		local all = workspace:GetDescendants()
		for i, inst in ipairs(all) do
			if inst:IsA("Model") then tryAddModel(inst) end
			if i % 200 == 0 then task.wait() end
		end
	end)

	workspace.DescendantAdded:Connect(function(inst)
		if inst:IsA("Model") then
			task.defer(function() if inst.Parent then tryAddModel(inst) end end)
		elseif inst:IsA("Humanoid") then
			local model = inst.Parent
			if model and model:IsA("Model") then tryAddModel(model) end
		end
	end)

	workspace.DescendantRemoving:Connect(function(inst)
		if inst:IsA("Model") then removeModel(inst) end
	end)

	-- ===== Collision / Anchor toggle =====
	local collisionDisabledModels = {}
	local anchorDisabledModels = {}

	local function setModelCollision(model, canCollide)
		for _, part in ipairs(model:GetDescendants()) do
			if part:IsA("BasePart") then part.CanCollide = canCollide end
		end
	end

	local function setModelAnchored(model, anchored)
		for _, part in ipairs(model:GetDescendants()) do
			if part:IsA("BasePart") then part.Anchored = anchored end
		end
	end

	local function restoreAllCollisions()
		for model in pairs(collisionDisabledModels) do
			if model.Parent then setModelCollision(model, true) end
		end
		collisionDisabledModels = {}
	end

	local function restoreAllAnchors()
		for model in pairs(anchorDisabledModels) do
			if model.Parent then setModelAnchored(model, false) end
		end
		anchorDisabledModels = {}
	end

	-- ===== Cluster pull =====
	local PULL_THRESHOLD = 2
	local FRONT_DISTANCE = 4
	local CLUSTER_RADIUS = 2.5
	local RING_GAP = 2
	local FIRST_RING_COUNT = 8

	local function getClusterOffset(index)
		if index == 0 then return Vector2.new(0, 0) end
		local ringIndex, slotsBefore, ringCapacity = 1, 0, FIRST_RING_COUNT
		while index > slotsBefore + ringCapacity do
			slotsBefore += ringCapacity
			ringIndex += 1
			ringCapacity = FIRST_RING_COUNT + (ringIndex - 1) * 4
		end
		local posInRing = index - slotsBefore - 1
		local angle = (posInRing / ringCapacity) * math.pi * 2
		local radius = CLUSTER_RADIUS + (ringIndex - 1) * RING_GAP
		return Vector2.new(math.cos(angle) * radius, math.sin(angle) * radius)
	end

	local function pullMobsOnce(rangeLimit)
		local character = player.Character
		if not character then return 0 end
		local hrp = character:FindFirstChild("HumanoidRootPart")
		if not hrp then return 0 end

		local hrpPos = hrp.Position
		local lookVector = hrp.CFrame.LookVector
		local rightVector = hrp.CFrame.RightVector
		local clusterCenter = hrpPos + (lookVector * FRONT_DISTANCE)

		local pulledCount, offset = 0, 0

local DEATH_CLEANUP_DELAY = 0.15 -- หน่วงก่อนลบ กันพลาด loot/เอฟเฟกต์ที่ยังไม่ทันเกิด
local pendingCleanup = {} -- กันลบซ้ำถ้ามอนตัวเดิมเข้าเงื่อนไข "ตาย" หลายรอบก่อนถูกลบจริง

for model, humanoid in pairs(cachedMobs) do
	if not model.Parent or not humanoid.Parent or humanoid.Health <= 0
		or humanoid:GetState() == Enum.HumanoidStateType.Dead then
		collisionDisabledModels[model] = nil
		anchorDisabledModels[model] = nil
		cachedMobs[model] = nil

		-- หน่วงสั้นๆ ก่อนลบซาก กันแลคจากมอนสเตอร์ที่ค้างอยู่ แต่ไม่ลบทันทีเผื่อ server ยังต้องใช้ตอนตาย
		if model.Parent and not pendingCleanup[model] then
			pendingCleanup[model] = true
			task.delay(DEATH_CLEANUP_DELAY, function()
				if model.Parent then
					pcall(function()
						model:Destroy()
					end)
				end
				pendingCleanup[model] = nil
			end)
		end
	else
				local mobPos = safeGetPivotPosition(model)
				if mobPos then
					local dist = (mobPos - hrpPos).Magnitude
					if (not rangeLimit) or dist <= rangeLimit then
						local clusterOffset = getClusterOffset(offset)
						local targetPos = clusterCenter + (lookVector * clusterOffset.Y) + (rightVector * clusterOffset.X)

						if not collisionDisabledModels[model] then
							setModelCollision(model, false)
							collisionDisabledModels[model] = true
						end
						if not anchorDisabledModels[model] then
							setModelAnchored(model, true)
							anchorDisabledModels[model] = true
						end

						if (mobPos - targetPos).Magnitude > PULL_THRESHOLD then
							pcall(function() model:PivotTo(CFrame.new(targetPos)) end)
						end
						pulledCount += 1
						offset += 1
					end
				end
			end
		end
		return pulledCount
	end

	-- ===== Loop =====
	local autoPulling, currentMode, heartbeatConn = false, nil, nil
	local PULL_INTERVAL, timeSinceLastPull = 0.03, 0

	local function resetButtons()
		pullAllButton.Text = "Start Pull All"
		pullAllButton.BackgroundColor3 = Theme.Success
		pullRangeButton.Text = "Start Pull Range"
		pullRangeButton.BackgroundColor3 = Theme.Button
	end

	local function stopAutoPull()
		if not autoPulling then return end
		autoPulling, currentMode = false, nil
		SetStatus("Stopped")
		resetButtons()
		if heartbeatConn then heartbeatConn:Disconnect(); heartbeatConn = nil end
		restoreAllCollisions()
		restoreAllAnchors()
	end

	local function startAutoPull(mode)
		stopAutoPull()
		autoPulling, currentMode, timeSinceLastPull = true, mode, 0

		if mode == "all" then
			pullAllButton.Text = "Stop Pull All"
			pullAllButton.BackgroundColor3 = Theme.Danger
		else
			pullRangeButton.Text = "Stop Pull Range"
			pullRangeButton.BackgroundColor3 = Theme.Danger
		end

		heartbeatConn = RunService.Heartbeat:Connect(function(dt)
			timeSinceLastPull += dt
			if timeSinceLastPull < PULL_INTERVAL then return end
			timeSinceLastPull = 0

			local rangeLimit = currentMode == "range" and tonumber(distanceBox.Text) or nil
			local count = pullMobsOnce(rangeLimit)

			if currentMode == "all" then
				SetStatus("Running - Pull All (" .. count .. ")")
			else
				SetStatus("Running - Pull Range " .. (rangeLimit or "?") .. " (" .. count .. ")")
			end
		end)
	end

	pullAllButton.MouseButton1Click:Connect(function()
		if autoPulling and currentMode == "all" then stopAutoPull() else startAutoPull("all") end
	end)

	pullRangeButton.MouseButton1Click:Connect(function()
		if autoPulling and currentMode == "range" then stopAutoPull() else startAutoPull("range") end
	end)

	-- ===== Range indicator =====
	local showRange = false
	local rangeIndicator = Instance.new("Part")
	rangeIndicator.Name = "RangeIndicator"
	rangeIndicator.Shape = Enum.PartType.Cylinder
	rangeIndicator.Anchored = true
	rangeIndicator.CanCollide = false
	rangeIndicator.CanQuery = false
	rangeIndicator.CastShadow = false
	rangeIndicator.Material = Enum.Material.Neon
	rangeIndicator.Color = Color3.fromRGB(80, 170, 255)
	rangeIndicator.Transparency = 0.75
	rangeIndicator.Size = Vector3.new(0.2, 10, 10)
	rangeIndicator.Parent = nil

	RunService.Heartbeat:Connect(function()
		if not showRange then
			if rangeIndicator.Parent then rangeIndicator.Parent = nil end
			return
		end
		local character = player.Character
		local hrp = character and character:FindFirstChild("HumanoidRootPart")
		if not hrp then rangeIndicator.Parent = nil; return end
		local dist = tonumber(distanceBox.Text)
		if not dist or dist <= 0 then rangeIndicator.Parent = nil; return end
		if rangeIndicator.Parent ~= workspace then rangeIndicator.Parent = workspace end
		local diameter = dist * 2
		rangeIndicator.Size = Vector3.new(0.2, diameter, diameter)
		local footPos = hrp.Position - Vector3.new(0, hrp.Size.Y / 2 + 0.1, 0)
		rangeIndicator.CFrame = CFrame.new(footPos) * CFrame.Angles(0, 0, math.rad(90))
	end)

	showRangeBtn.MouseButton1Click:Connect(function()
		showRange = not showRange
		showRangeBtn.Text = showRange and "☑ Show Range" or "☐ Show Range"
		showRangeBtn.BackgroundColor3 = showRange and Theme.Button or Color3.fromRGB(55, 55, 55)
	end)

	-- หยุดลูปและลบ range indicator ตอนปิด GUI ทั้งหมด (ผูกไว้ด้านล่าง)
	screenGui.AncestryChanged:Connect(function(_, parent)
		if not parent then
			stopAutoPull()
			rangeIndicator:Destroy()
		end
	end)
end

-- ═══════════════════════════════════════════
-- DRAGGABLE
-- ═══════════════════════════════════════════
local dragging, dragStart, startPos = false, nil, nil

local function updateDrag(input)
	local delta = input.Position - dragStart
	mainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

titleBar.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging = true
		dragStart = input.Position
		startPos = mainFrame.Position
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then dragging = false end
		end)
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
		updateDrag(input)
	end
end)

-- ═══════════════════════════════════════════
-- MINIMIZE / CLOSE
-- ═══════════════════════════════════════════
local minimized = false
local expandedSize = mainFrame.Size

minimizeBtn.MouseButton1Click:Connect(function()
	minimized = not minimized
	bodyFrame.Visible = not minimized
	statusBar.Visible = not minimized

	local targetSize = minimized and UDim2.new(0, expandedSize.X.Offset, 0, 38) or expandedSize
	TweenService:Create(mainFrame, TweenInfo.new(0.2, Enum.EasingStyle.Quad), {Size = targetSize}):Play()
end)

closeBtn.MouseButton1Click:Connect(function()
	local tw = TweenService:Create(mainFrame, TweenInfo.new(0.2), {BackgroundTransparency = 1})
	for _, desc in ipairs(mainFrame:GetDescendants()) do
		if desc:IsA("Frame") or desc:IsA("TextButton") or desc:IsA("ScrollingFrame") then
			TweenService:Create(desc, TweenInfo.new(0.15), {BackgroundTransparency = 1}):Play()
		end
	end
	tw:Play()
	tw.Completed:Wait()
	screenGui:Destroy()
end)

-- ═══════════════════════════════════════════
-- OPEN ANIMATION (Fade-in) + เริ่มที่หน้า Stats
-- ═══════════════════════════════════════════
mainFrame.BackgroundTransparency = 1
TweenService:Create(mainFrame, TweenInfo.new(0.25), {BackgroundTransparency = 0}):Play()

SwitchPage("Stats")
