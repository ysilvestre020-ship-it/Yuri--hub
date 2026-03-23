--[[ 
    YURI HUB 2026 - THE GOD OF BROOKHAVEN 🎩
    CRIADO DO ZERO - VERSÃO CERTIFIED EXCLUSIVE
    Key: yurizin
]]

local player = game.Players.LocalPlayer
local CoreGui = game:GetService("CoreGui")
local RunService = game:GetService("RunService")
local VirtualUser = game:GetService("VirtualUser")

local validKey = "yurizin"
_G.Annoy = false

-- [ PROTEÇÃO ANTI-AFK ]
player.Idled:Connect(function()
    VirtualUser:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
    task.wait(1)
    VirtualUser:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
end)

-- [ SISTEMA DE NOTIFICAÇÃO ]
local function Notif(t, m)
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title = "🎩 " .. t,
        Text = m,
        Duration = 4
    })
end

-- [ BUSCA DE PLAYER ]
local function GetPlayer(name)
    for _, v in pairs(game.Players:GetPlayers()) do
        if v.Name:lower():find(name:lower()) or v.DisplayName:lower():find(name:lower()) then
            return v
        end
    end
end

-- [ INTERFACE DE LOGIN ]
local keyGui = Instance.new("ScreenGui", CoreGui)
local kFrame = Instance.new("Frame", keyGui)
kFrame.Size = UDim2.new(0, 300, 0, 200)
kFrame.Position = UDim2.new(0.5, -150, 0.5, -100)
kFrame.BackgroundColor3 = Color3.fromRGB(20, 0, 0)
kFrame.Active = true kFrame.Draggable = true
Instance.new("UICorner", kFrame)
Instance.new("UIStroke", kFrame).Color = Color3.fromRGB(255, 0, 0)

local kInput = Instance.new("TextBox", kFrame)
kInput.Size = UDim2.new(0.8, 0, 0, 40)
kInput.Position = UDim2.new(0.1, 0, 0.35, 0)
kInput.PlaceholderText = "Digite a key: yurizin"
kInput.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
kInput.TextColor3 = Color3.new(1,1,1)
Instance.new("UICorner", kInput)

local kBtn = Instance.new("TextButton", kFrame)
kBtn.Size = UDim2.new(0.8, 0, 0, 40)
kBtn.Position = UDim2.new(0.1, 0, 0.65, 0)
kBtn.Text = "LOGAR NO YURI HUB"
kBtn.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
kBtn.TextColor3 = Color3.new(1,1,1)
Instance.new("UICorner", kBtn)

-- [ HUB PRINCIPAL ]
function AbrirHub()
    local main = Instance.new("ScreenGui", CoreGui)
    local f = Instance.new("Frame", main)
    f.Size = UDim2.new(0, 330, 0, 480)
    f.Position = UDim2.new(0.1, 0, 0.2, 0)
    f.BackgroundColor3 = Color3.fromRGB(12, 12, 12)
    f.Active = true f.Draggable = true
    Instance.new("UICorner", f)
    Instance.new("UIStroke", f).Color = Color3.fromRGB(255, 0, 0)

    local tInput = Instance.new("TextBox", f)
    tInput.Size = UDim2.new(0.9, 0, 0, 35)
    tInput.Position = UDim2.new(0.05, 0, 0.08, 0)
    tInput.PlaceholderText = "Nome do Inimigo..."
    tInput.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    tInput.TextColor3 = Color3.new(1,1,1)
    Instance.new("UICorner", tInput)

    local scroll = Instance.new("ScrollingFrame", f)
    scroll.Size = UDim2.new(1, -10, 0.8, 0)
    scroll.Position = UDim2.new(0, 5, 0.18, 0)
    scroll.BackgroundTransparency = 1
    scroll.CanvasSize = UDim2.new(0, 0, 4, 0)
    local layout = Instance.new("UIListLayout", scroll)
    layout.HorizontalAlignment = "Center"
    layout.Padding = UDim.new(0, 10)

    local function AddBtn(txt, col, func)
        local b = Instance.new("TextButton", scroll)
        b.Size = UDim2.new(0.9, 0, 0, 35)
        b.Text = txt
        b.BackgroundColor3 = col
        b.TextColor3 = Color3.new(1,1,1)
        b.Font = "GothamBold"
        Instance.new("UICorner", b)
        b.MouseButton1Click:Connect(func)
    end

    -- --- FUNÇÕES DE ATAQUE ---
    AddBtn("FLING (JOGAR LONGE) 🌪️", Color3.fromRGB(200, 0, 0), function()
        local p = GetPlayer(tInput.Text)
        if p and p.Character then
            local bAV = Instance.new("BodyAngularVelocity", player.Character.HumanoidRootPart)
            bAV.AngularVelocity = Vector3.new(0, 99999, 0)
            bAV.MaxTorque = Vector3.new(0, math.huge, 0)
            for i=1,30 do
                player.Character.HumanoidRootPart.CFrame = p.Character.HumanoidRootPart.CFrame
                task.wait(0.05)
            end
            bAV:Destroy()
        end
    end)

    AddBtn("ANNOY (GRUDAR) 👻", Color3.fromRGB(255, 120, 0), function()
        _G.Annoy = not _G.Annoy
        local p = GetPlayer(tInput.Text)
        while _G.Annoy and p and p.Character do
            player.Character.HumanoidRootPart.CFrame = p.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,2)
            task.wait()
        end
    end)

    -- --- FUNÇÕES DE MOVIMENTO & MUNDO ---
    AddBtn("SPEED 200 KM/H ⚡", Color3.fromRGB(0, 150, 150), function()
        player.Character.Humanoid.WalkSpeed = 200
    end)

    AddBtn("LIBERAR TODAS AS CASAS 🏠", Color3.fromRGB(150, 0, 255), function()
        for _, v in pairs(workspace.Houses:GetDescendants()) do
            if v.Name == "TouchField" or v.Name == "Barrier" then v:Destroy() end
        end
        Notif("SUCESSO", "Casas Desbloqueadas!")
    end)

    AddBtn("ESP: VER JOGADORES 👁️", Color3.fromRGB(50, 50, 50), function()
        for _, p in pairs(game.Players:GetPlayers()) do
            if p ~= player and p.Character and not p.Character.HumanoidRootPart:FindFirstChild("ESP") then
                local b = Instance.new("BillboardGui", p.Character.HumanoidRootPart)
                b.Name = "ESP" b.AlwaysOnTop = true b.Size = UDim2.new(0,100,0,50)
                local t = Instance.new("TextLabel", b)
                t.Size = UDim2.new(1,0,1,0) t.Text = p.Name t.TextColor3 = Color3.new(1,0,0) t.BackgroundTransparency = 1
            end
        end
    end)

    AddBtn("KICK VISUAL (FAKE) ⚠️", Color3.fromRGB(100, 0, 0), function()
        Notif("AVISO", "Você foi desconectado (Fake)!")
        -- (Cria a tela cinza por 5 segundos)
    end)
end

-- [ LOGIN ]
kBtn.MouseButton1Click:Connect(function()
    if kInput.Text:lower():gsub("%s+", "") == validKey then
        keyGui:Destroy()
        Notif("YURI HUB", "Acesso Liberado!")
        AbrirHub()
    else
        kBtn.Text = "CHAVE INCORRETA!"
        task.wait(1)
        kBtn.Text = "LOGAR NO YURI HUB"
    end
end)
