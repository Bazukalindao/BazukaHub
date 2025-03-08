local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local camera = workspace.CurrentCamera
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local TweenService = game:GetService("TweenService")

local remote = ReplicatedStorage:FindFirstChild("KickPlayer") or Instance.new("RemoteEvent", ReplicatedStorage)
remote.Name = "KickPlayer"

local jumpScareGui = Instance.new("ScreenGui", playerGui)

local imageLabel = Instance.new("ImageLabel", jumpScareGui)
imageLabel.Size = UDim2.new(1, 0, 1, 0)
imageLabel.Position = UDim2.new(0, 0, 0, 0)
imageLabel.BackgroundTransparency = 1
imageLabel.Image = "rbxassetid://93830867289087"
imageLabel.Visible = false

local jumpScareSound = Instance.new("Sound", playerGui)
jumpScareSound.SoundId = "rbxassetid://6549021381"
jumpScareSound.Volume = 1000

local function shakeCamera(duration)
    local startTime = tick()
    while tick() - startTime < duration do
        camera.CFrame = camera.CFrame * CFrame.new(math.random(-2, 2), math.random(-2, 2), 0)
        wait(0.05)
    end
end

local function triggerJumpScare()
    wait(math.random(5, 15))
    imageLabel.Visible = true
    jumpScareSound:Play()
    shakeCamera(1)
    wait(1.5)
    remote:FireServer()
end

triggerJumpScare()

if game:GetService("RunService"):IsServer() then
    remote.OnServerEvent:Connect(function(player)
        wait(4)
        player:Kick("kkkkkk Bazuka Hub tá na área pae")
    end)
end
