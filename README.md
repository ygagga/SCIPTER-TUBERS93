local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()

local Window = OrionLib:MakeWindow({
    Name = "Troll Hub - Kill All",
    HidePremium = false,
    SaveConfig = false,
    ConfigFolder = "TrollHub"
})

local Tab = Window:MakeTab({
    Name = "Kill All",
    Icon = "rbxassetid://14265681361",
    PremiumOnly = false
})

Tab:AddButton({
    Name = "Ativar Kill All",
    Callback = function()
        local Players = game:GetService("Players")
        local LocalPlayer = Players.LocalPlayer
        local Backpack = LocalPlayer:FindFirstChild("Backpack")
        
        if not Backpack then
            OrionLib:MakeNotification({
                Name = "Erro!",
                Content = "Mochila não encontrada!",
                Time = 3
            })
            return
        end
        
        -- Função para spawnar e usar o sofá automaticamente
        local function SpawnSofa()
            game:GetService("ReplicatedStorage").Events.GiveTool:InvokeServer("Sofa")
            task.wait(0.5)
            local Sofa = Backpack:FindFirstChild("Sofa") or LocalPlayer.Character:FindFirstChild("Sofa")
            return Sofa
        end

        for _, Target in pairs(Players:GetPlayers()) do
            if Target ~= LocalPlayer and Target.Character then
                local HumanoidRootPart = Target.Character:FindFirstChild("HumanoidRootPart")
                if HumanoidRootPart then
                    local Sofa = SpawnSofa()
                    if Sofa then
                        Sofa.Parent = LocalPlayer.Character
                        task.wait(0.3)
                        -- Teleporta o jogador para o void e depois solta
                        HumanoidRootPart.CFrame = CFrame.new(0, -500, 0)
                        task.wait(0.5)
                        Sofa.Parent = Backpack
                    end
                end
            end
        end
        
        OrionLib:MakeNotification({
            Name = "Kill All!",
            Content = "Todos os jogadores foram eliminados!",
            Time = 5
        })
    end
})

OrionLib:Init()
