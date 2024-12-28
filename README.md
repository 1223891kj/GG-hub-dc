-- GG Hub [UNIVERSAL]
-- Script para Roblox Executor Delta

local GGHub = Instance.new("ScreenGui")
local OpenCloseButton = Instance.new("TextButton")
local MainFrame = Instance.new("Frame")
local ESPPlayersButton = Instance.new("TextButton")
local SpectatePlayersButton = Instance.new("TextButton")
local UpdateListButton = Instance.new("TextButton")
local PlayersList = Instance.new("ScrollingFrame")
local Title = Instance.new("TextLabel")

-- Propriedades do GGHub
GGHub.Name = "GGHub"
GGHub.Parent = game.CoreGui

-- Botão de abrir/fechar
OpenCloseButton.Name = "OpenCloseButton"
OpenCloseButton.Parent = GGHub
OpenCloseButton.BackgroundColor3 = Color3.fromRGB(128, 0, 128) -- Roxo
OpenCloseButton.Position = UDim2.new(0, 0, 0.5, 0)
OpenCloseButton.Size = UDim2.new(0, 200, 0, 50)
OpenCloseButton.Font = Enum.Font.SourceSans
OpenCloseButton.Text = "GG Hub"
OpenCloseButton.TextColor3 = Color3.fromRGB(255, 0, 0) -- Vermelho
OpenCloseButton.TextSize = 24

-- Frame principal
MainFrame.Name = "MainFrame"
MainFrame.Parent = GGHub
MainFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 0) -- Amarelo
MainFrame.Position = UDim2.new(0.5, -200, 0.5, -200)
MainFrame.Size = UDim2.new(0, 400, 0, 400)
MainFrame.Visible = false

-- Título
Title.Name = "Title"
Title.Parent = MainFrame
Title.BackgroundColor3 = Color3.fromRGB(255, 255, 0)
Title.Size = UDim2.new(1, 0, 0, 50)
Title.Font = Enum.Font.SourceSans
Title.Text = "GG HUB [UNIVERSAL]"
Title.TextColor3 = Color3.fromRGB(255, 0, 0) -- Vermelho
Title.TextSize = 24

-- Botão ESP Players
ESPPlayersButton.Name = "ESPPlayersButton"
ESPPlayersButton.Parent = MainFrame
ESPPlayersButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0) -- Vermelho
ESPPlayersButton.Position = UDim2.new(0.1, 0, 0.2, 0)
ESPPlayersButton.Size = UDim2.new(0.8, 0, 0, 50)
ESPPlayersButton.Font = Enum.Font.SourceSans
ESPPlayersButton.Text = "ESP Players"
ESPPlayersButton.TextColor3 = Color3.fromRGB(0, 0, 0) -- Preto
ESPPlayersButton.TextSize = 24

-- Botão Spectate Players
SpectatePlayersButton.Name = "SpectatePlayersButton"
SpectatePlayersButton.Parent = MainFrame
SpectatePlayersButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0) -- Vermelho
SpectatePlayersButton.Position = UDim2.new(0.1, 0, 0.4, 0)
SpectatePlayersButton.Size = UDim2.new(0.8, 0, 0, 50)
SpectatePlayersButton.Font = Enum.Font.SourceSans
SpectatePlayersButton.Text = "Spectate Players"
SpectatePlayersButton.TextColor3 = Color3.fromRGB(0, 0, 0) -- Preto
SpectatePlayersButton.TextSize = 24

-- Botão Update List
UpdateListButton.Name = "UpdateListButton"
UpdateListButton.Parent = MainFrame
UpdateListButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0) -- Vermelho
UpdateListButton.Position = UDim2.new(0.1, 0, 0.6, 0)
UpdateListButton.Size = UDim2.new(0.8, 0, 0, 50)
UpdateListButton.Font = Enum.Font.SourceSans
UpdateListButton.Text = "Update List"
UpdateListButton.TextColor3 = Color3.fromRGB(0, 0, 0) -- Preto
UpdateListButton.TextSize = 24

-- Lista de jogadores
PlayersList.Name = "PlayersList"
PlayersList.Parent = MainFrame
PlayersList.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
PlayersList.Position = UDim2.new(0.1, 0, 0.8, 0)
PlayersList.Size = UDim2.new(0.8, 0, 0, 100)
PlayersList.CanvasSize = UDim2.new(0, 0, 2, 0)

-- Função para abrir/fechar o Hub
OpenCloseButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

-- Função para atualizar a lista de jogadores
local function UpdatePlayersList()
    PlayersList:ClearAllChildren()
    for _, player in pairs(game.Players:GetPlayers()) do
        local PlayerButton = Instance.new("TextButton")
        PlayerButton.Parent = PlayersList
        PlayerButton.Size = UDim2.new(1, 0, 0, 50)
        PlayerButton.Text = player.Name
        PlayerButton.TextColor3 = Color3.fromRGB(0, 0, 0)
        PlayerButton.TextSize = 24
        PlayerButton.MouseButton1Click:Connect(function()
            -- Função de spectate
        end)
    end
end

UpdateListButton.MouseButton1Click:Connect(UpdatePlayersList)

-- Função para ESP Players
ESPPlayersButton.MouseButton1Click:Connect(function()
    -- Função de ESP
end)

-- Inicializar a lista de jogadores
UpdatePlayersList()

-- Função para ESP Players
local function EnableESP()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer then
            local BillboardGui = Instance.new("BillboardGui")
            local TextLabel = Instance.new("TextLabel")

            BillboardGui.Name = "ESP"
            BillboardGui.Adornee = player.Character.Head
            BillboardGui.Size = UDim2.new(0, 100, 0, 50)
            BillboardGui.StudsOffset = Vector3.new(0, 3, 0)
            BillboardGui.AlwaysOnTop = true

            TextLabel.Parent = BillboardGui
            TextLabel.Size = UDim2.new(1, 0, 1, 0)
            TextLabel.BackgroundTransparency = 1
            TextLabel.Text = player.Name
            TextLabel.TextColor3 = Color3.fromRGB(255, 0, 0) -- Vermelho
            TextLabel.TextSize = 14

            BillboardGui.Parent = player.Character.Head
        end
    end
end

ESPPlayersButton.MouseButton1Click:Connect(EnableESP)

-- Função para Spectate Players
local function SpectatePlayer(player)
    local camera = game.Workspace.CurrentCamera
    camera.CameraSubject = player.Character.Humanoid
end

local function StopSpectating()
    local camera = game.Workspace.CurrentCamera
    camera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
end

local spectating = false
local spectateTarget = nil

SpectatePlayersButton.MouseButton1Click:Connect(function()
    if spectating then
        StopSpectating()
        spectating = false
    else
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer then
                local PlayerButton = Instance.new("TextButton")
                PlayerButton.Parent = PlayersList
                PlayerButton.Size = UDim2.new(1, 0, 0, 50)
                PlayerButton.Text = player.Name
                PlayerButton.TextColor3 = Color3.fromRGB(0, 0, 0)
                PlayerButton.TextSize = 24
                PlayerButton.MouseButton1Click:Connect(function()
                    if spectateTarget == player then
                        StopSpectating()
                        spectateTarget = nil
                        spectating = false
                    else
                        SpectatePlayer(player)
                        spectateTarget = player
                        spectating = true
                    end
                end)
            end
        end
    end
end)

