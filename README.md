local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

OrionLib:MakeNotification({
	Name = "Hi rei made this",
	Content = "k LIAR",
	Image = "rbxassetid://4483345998",
	Time = 5
})


local Window = OrionLib:MakeWindow({Name = "Shalom!", HidePremium = false, SaveConfig = true, ConfigFolder = "Orion"})

--Player Tab--

local PlayerTab = Window:MakeTab({
	Name = "Fishy",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

local PlayerSection = PlayerTab:AddSection({
	Name = "Fishy"
})


PlayerSection:AddButton({
	Name = "Cast Auto (click when fish caught)",
	Callback = function(Value)
local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local reel = playerGui:WaitForChild("reel")
local bar = reel:WaitForChild("bar")
local fish = bar:WaitForChild("fish")
local playerbar = bar:WaitForChild("playerbar")

local runService = game:GetService("RunService")

local function updatePlayerBarPosition()
    runService.Heartbeat:Connect(function()
        local fishPosition = fish.Position
        playerbar.Position = fishPosition
    end)
end

updatePlayerBarPosition()


userInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if input.KeyCode == Enum.KeyCode.B and not gameProcessedEvent then
        updatePlayerBarPosition()
    end
end)

	end    
})

PlayerSection:AddButton({
	Name = "Shake Middle (press f when casted)",
	Callback = function(Value)
local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local userInputService = game:GetService("UserInputService")
local runService = game:GetService("RunService")

local function moveButtonToCenter(button)
    if button then
        button.Position = UDim2.new(0.5, -button.Size.X.Offset / 2, 0.5, -button.Size.Y.Offset / 2)
    end
end

local function startButtonPositioning()
    local shakeui = playerGui:WaitForChild("shakeui", 25)
    local safezoneui = shakeui:WaitForChild("safezone", 25)

    runService.Heartbeat:Connect(function()
        local button = safezoneui:FindFirstChild("button")
        
        if button then
            moveButtonToCenter(button)
        end
    end)
end

userInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if input.KeyCode == Enum.KeyCode.F and not gameProcessedEvent then
        startButtonPositioning()
    end
end)
	end    
})



--Player Tab End--

--Settings Tab--

local SettingsTab = Window:MakeTab({
	Name = "Settings",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

local SettingsSection = SettingsTab:AddSection({
	Name = "Settings"
})

SettingsSection:AddButton({
	Name = "Destroy UI",
	Callback = function()
        OrionLib:Destroy()
  	end    
})

--Settings End--

OrionLib:Init() --UI Lib End
