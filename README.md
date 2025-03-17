-- Carregar a Orion Library
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

-- Criando a Interface
local Window = OrionLib:MakeWindow({
    Name = "Cartola Hub V2",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "CartolaHub"
})

-- Criando a Aba Principal
local MainTab = Window:MakeTab({
    Name = "Funções",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Variável de jogador selecionado
local selectedPlayer = ""

-- 🏹 SELEÇÃO DE JOGADOR
MainTab:AddTextbox({
    Name = "Nome do Jogador",
    Default = "",
    TextDisappear = true,
    Callback = function(value)
        selectedPlayer = value
    end
})

-- 🚀 TELEPORTAR TODOS PARA VOCÊ
MainTab:AddButton({
    Name = "Teleportar Todos para Mim",
    Callback = function()
        local players = game:GetService("Players")
        local localPlayer = players.LocalPlayer
        local root = localPlayer.Character and localPlayer.Character:FindFirstChild("HumanoidRootPart")

        if root then
            for _, target in pairs(players:GetPlayers()) do
                if target.Character and target ~= localPlayer then
                    local targetRoot = target.Character:FindFirstChild("HumanoidRootPart")
                    if targetRoot then
                        targetRoot.CFrame = root.CFrame
                    end
                end
            end
        end
    end
})

-- 👀 SPECTATE
MainTab:AddButton({
    Name = "Espectar Jogador",
    Callback = function()
        local players = game:GetService("Players")
        local target = players:FindFirstChild(selectedPlayer)

        if target and target.Character then
            game.Workspace.CurrentCamera.CameraSubject = target.Character:FindFirstChildOfClass("Humanoid")
        end
    end
})

MainTab:AddButton({
    Name = "Parar de Espectar",
    Callback = function()
        game.Workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    end
})

-- 🎵 TOCAR ÁUDIO GLOBALMENTE
local musicId = ""
MainTab:AddTextbox({
    Name = "ID do Áudio",
    Default = "",
    TextDisappear = true,
    Callback = function(value)
        musicId = value
    end
})

MainTab:AddButton({
    Name = "Tocar Música 📢",
    Callback = function()
        if musicId ~= "" then
            local sound = Instance.new("Sound", game.Workspace)
            sound.SoundId = "rbxassetid://" .. musicId
            sound.Volume = 10
            sound.Looped = true
            sound:Play()
        end
    end
})

MainTab:AddButton({
    Name = "Parar Música ⛔",
    Callback = function()
        for _, obj in pairs(game.Workspace:GetChildren()) do
            if obj:IsA("Sound") then
                obj:Stop()
                obj:Destroy()
            end
        end
    end
})

-- 🔄 FLING PLAYER
MainTab:AddButton({
    Name = "Fling Jogador",
    Callback = function()
        local players = game:GetService("Players")
        local target = players:FindFirstChild(selectedPlayer)

        if target and target.Character then
            local root = target.Character:FindFirstChild("HumanoidRootPart")
            if root then
                local bodyVelocity = Instance.new("BodyVelocity", root)
                bodyVelocity.Velocity = Vector3.new(0, 500, 0)
                bodyVelocity.MaxForce = Vector3.new(1e5, 1e5, 1e5)
                wait(1)
                bodyVelocity:Destroy()
            end
        end
    end
})

-- ☠️ KILL ALL (Sofá no Void)
MainTab:AddButton({
    Name = "Kill All (Sofá no Void)",
    Callback = function()
        local players = game:GetService("Players")
        local localPlayer = players.LocalPlayer

        for _, target in pairs(players:GetPlayers()) do
            if target ~= localPlayer and target.Character then
                local humanoidRoot = target.Character:FindFirstChild("HumanoidRootPart")
                if humanoidRoot then
                    -- Spawnar um sofá e prender o jogador
                    local sofa = Instance.new("Part", game.Workspace)
                    sofa.Size = Vector3.new(4, 2, 2)
                    sofa.Position = humanoidRoot.Position + Vector3.new(0, 2, 0)
                    sofa.Anchored = false

                    -- Criar soldagem entre o sofá e o jogador
                    local weld = Instance.new("WeldConstraint", sofa)
                    weld.Part0 = sofa
                    weld.Part1 = humanoidRoot

                    -- Jogar no Void
                    wait(1)
                    humanoidRoot.CFrame = CFrame.new(0, -500, 0)
                end
            end
        end
    end
})

-- ℹ️ INFORMAÇÕES
local AboutTab = Window:MakeTab({
    Name = "Sobre",
    Icon = "rbxassetid://6034509992",
    PremiumOnly = false
})

AboutTab:AddParagraph("Cartola Hub V2", "Script recriado com base no original do Renegado_666. Feito para trollar no Brookhaven RP!")

OrionLib:Init()
