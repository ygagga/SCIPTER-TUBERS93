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


local Tabs = {
    Main = Window:AddTab({ Title = "Test" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })

    
}


Tabs.Main:AddButton({ Title = "test", Callback = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/ygagga/ESP-NAME-kkkk/refs/heads/main/README.md"))() end }
