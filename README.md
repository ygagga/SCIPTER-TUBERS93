-- Carregar a Orion Library
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

-- Criar a Janela Principal
local Window = OrionLib:MakeWindow({
    Name = "👾 ZenithCore - Troll 👾",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "ZenithCore"
})

-- Criar a Aba de Troll
local TrollTab = Window:MakeTab({
    Name = "Troll",
    Icon = "rbxassetid://4483362458",
    PremiumOnly = false
})

-- Criar a Seção de Kill All
TrollTab:AddSection({
    Name = "Kill All"
})

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

function KillPlayer(target)
    if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
        -- Pegar um sofá automaticamente
        local args = {
            [1] = "Give",
            [2] = "Couch"
        }
        game:GetService("ReplicatedStorage"):FindFirstChild("Interaction"):FireServer(unpack(args))

        task.wait(0.5) -- Pequeno delay para garantir que o sofá foi pego

        -- Pegar o alvo com o sofá
        local humanoidRoot = target.Character:FindFirstChild("HumanoidRootPart")
        if humanoidRoot then
            humanoidRoot.CFrame = CFrame.new(0, -500, 0) -- Joga no Void
        end
    end
end

function KillAll()
    for _, target in pairs(Players:GetPlayers()) do
        if target ~= LocalPlayer then
            KillPlayer(target)
            task.wait(0.5) -- Pequeno delay para não bugar
        end
    end
end

-- Botão de Kill All
TrollTab:AddButton({
    Name = "Executar Kill All ☠️",
    Callback = function()
        KillAll()
    end
})

-- Finalizar e exibir GUI
OrionLib:Init()
