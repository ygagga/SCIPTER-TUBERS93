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
local ESPSection = ESP:NewSection("ESP Options")

-- Primeiro ESP (do GitHub)
ESPSection:NewButton("Activate ESP (GitHub)", "See players through walls (GitHub version)", function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/ygagga/ESP-AURA/refs/heads/main/README.md"))()
end)

-- Segundo ESP (Personalizado)
ESPSection:NewButton("Activate ESP (Custom)", "See players through walls (Custom version)", function()
    local function CreateESP(player)
        if player == game.Players.LocalPlayer then return end -- Evita que o ESP apareça no próprio jogador

        local highlight = Instance.new("Highlight")
        highlight.Parent = player.Character
        highlight.Adornee = player.Character
        highlight.FillColor = Color3.fromRGB(255, 0, 0) -- Cor vermelha para destaque
        highlight.OutlineColor = Color3.fromRGB(255, 255, 255) -- Contorno branco
        highlight.FillTransparency = 0.5
        highlight.OutlineTransparency = 0
    end

    local function EnableESP()
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character then
                CreateESP(player)
            end
        end

        -- Atualiza o ESP caso novos jogadores entrem no jogo
        game.Players.PlayerAdded:Connect(function(player)
            player.CharacterAdded:Connect(function()
                CreateESP(player)
            end)
        end)
    end

    EnableESP()
end)
