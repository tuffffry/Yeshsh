local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local HopButton = Instance.new("TextButton")
local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local TeleportService = game:GetService("TeleportService")

-- Set up the ScreenGui
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Set up the Frame
Frame.Size = UDim2.new(0.3, 0, 0.3, 0)
Frame.Position = UDim2.new(0.35, 0, 0.35, 0)
Frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
Frame.Parent = ScreenGui

-- Set up the Hop Button
HopButton.Size = UDim2.new(1, 0, 1, 0)
HopButton.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
HopButton.Text = "Hop to Next Server"
HopButton.Parent = Frame

-- Function to hop to the next server
local function hopToNextServer()
    local placeId = game.PlaceId
    local url = "https://games.roblox.com/v1/games/" .. placeId .. "/servers/Public?sortOrder=Asc&limit=100"
    
    local success, response = pcall(function()
        return HttpService:GetAsync(url)
    end)

    if success then
        local data = HttpService:JSONDecode(response)
        local servers = data.data

        if #servers > 0 then
            local randomServer = servers[math.random(1, #servers)]
            TeleportService:TeleportToPlaceInstance(placeId, randomServer.id, Players.LocalPlayer)
        else
            warn("No available servers to join.")
        end
    else
        warn("Failed to get server data: " .. response)
    end
end

-- Connect the button click to the hop function
HopButton.MouseButton1Click:Connect(hopToNextServer)
