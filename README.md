local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Tubers Hub | made by Shelby", "Sentinel")

-- Aba Home
local Home = Window:NewTab("Home")
local HomeSection = Home:NewSection("Home")

HomeSection:NewLabel("Welcome, User!")
HomeSection:NewLabel("This script made by Shelby")
HomeSection:NewLabel("version 1.7")

-- Aba Player
local Player = Window:NewTab("Player")
local PlayerSection = Player:NewSection("Player")

PlayerSection:NewSlider("Walkspeed", "Changes the walkspeed", 250, 16, function(s)
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = s
end)

PlayerSection:NewSlider("Jumppower", "Changes the jumppower", 250, 50, function(j)
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = j
end)

PlayerSection:NewButton("Inf Jumps", "Enables Inf Jumps", function()
    local InfiniteJumpEnabled = true
    game:GetService("UserInputService").JumpRequest:connect(function()
        if InfiniteJumpEnabled then
            game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Humanoid"):ChangeState("Jumping")
        end
    end)
end)

-- Aba ESP
local ESP = Window:NewTab("ESP")
local ESPSection = Player:NewSection("ESP")

ESPSection:NewButton("Inf ESP", "Enables Inf ESP", function()
    local players = game.Players:GetChildren("UserInputPlayers")

for _, player in pairs(players) do
    if player.Name ~= game.Players.LocalPlayer.Name then
        if player.Humanoid then
            if not player:FindFirstChild("Highlight") then
                local highlight = Instance.new('Highlight')
                highlight.Parent = player
                highlight.FaceColor = Color3.new(255, 255, 255) -- Change this to the desired color
                highlight.Transparency = 0.5 -- Change this to the desired transparency
            end
        end)
    end)
   


   
