-- NATAN DEAD REAILS 1.0 - HUB ESTILO KICIAHOOK

local Players = game:GetService("Players")
local plr = Players.LocalPlayer
local char = plr.Character or plr.CharacterAdded:Wait()

-- Criar GUI principal
local gui = Instance.new("ScreenGui", plr.PlayerGui)
gui.Name = "NATAN_DEAD_REAILS"
gui.ResetOnSpawn = false

-- Botão de abrir/fechar
local toggle = Instance.new("TextButton", gui)
toggle.Size = UDim2.new(0, 120, 0, 35)
toggle.Position = UDim2.new(0, 10, 0.4, 0)
toggle.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
toggle.Text = "Abrir Menu"
toggle.TextColor3 = Color3.new(1, 0, 0)
toggle.TextScaled = true
toggle.Font = Enum.Font.GothamBold

-- Menu principal
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 400, 0, 300)
frame.Position = UDim2.new(0, 140, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
frame.Visible = false

-- Título
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 40)
title.Text = "NATAN DEAD REAILS 1.0"
title.TextColor3 = Color3.fromRGB(255, 0, 0)
title.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
title.TextScaled = true
title.Font = Enum.Font.GothamBlack

-- Abas
local tabHolder = Instance.new("Frame", frame)
tabHolder.Size = UDim2.new(0, 100, 1, -40)
tabHolder.Position = UDim2.new(0, 0, 0, 40)
tabHolder.BackgroundColor3 = Color3.fromRGB(25, 25, 25)

local contentHolder = Instance.new("Frame", frame)
contentHolder.Size = UDim2.new(1, -100, 1, -40)
contentHolder.Position = UDim2.new(0, 100, 0, 40)
contentHolder.BackgroundColor3 = Color3.fromRGB(35, 35, 35)

-- Função criar botão de aba
local function createTab(name, contentFunc)
    local btn = Instance.new("TextButton", tabHolder)
    btn.Size = UDim2.new(1, 0, 0, 40)
    btn.Text = name
    btn.BackgroundColor3 = Color3.fromHSV(math.random(), 1, 1)
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.TextScaled = true
    btn.Font = Enum.Font.GothamBold

    btn.MouseButton1Click:Connect(function()
        for _, c in pairs(contentHolder:GetChildren()) do if c:IsA("Frame") then c.Visible = false end end
        contentFunc().Visible = true
    end)
end

-- Criação do conteúdo da aba de teleportes
local function teleportTab()
    local teleFrame = Instance.new("Frame", contentHolder)
    teleFrame.Size = UDim2.new(1, 0, 1, 0)
    teleFrame.BackgroundTransparency = 1
    teleFrame.Visible = false

    local locations = {
        {"Trem", Vector3.new(0, 10, 0)},
        {"Base 1", Vector3.new(100, 10, 100)},
        {"Base 2", Vector3.new(300, 10, 300)},
        {"Final", Vector3.new(1000, 10, 1000)}
    }

    for i, loc in pairs(locations) do
        local btn = Instance.new("TextButton", teleFrame)
        btn.Size = UDim2.new(0, 250, 0, 30)
        btn.Position = UDim2.new(0, 10, 0, (i-1)*35 + 10)
        btn.Text = "Teleporte: " .. loc[1]
        btn.BackgroundColor3 = Color3.fromHSV(math.random(), 1, 1)
        btn.TextColor3 = Color3.new(1, 1, 1)
        btn.TextScaled = true
        btn.Font = Enum.Font.GothamBold

        btn.MouseButton1Click:Connect(function()
            local hrp = plr.Character and plr.Character:FindFirstChild("HumanoidRootPart")
            if hrp then hrp.CFrame = CFrame.new(loc[2]) end
        end)
    end

    return teleFrame
end

-- Adiciona a aba "Teleportes"
createTab("Teleportes", teleportTab)

-- Função para abrir/fechar o menu
local open = false
toggle.MouseButton1Click:Connect(function()
    open = not open
    frame.Visible = open
    toggle.Text = open and "Fechar Menu" or "Abrir Menu"
end)
