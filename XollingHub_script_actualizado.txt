-- XollingHub v1.0 | Script personalizado by Mario

--// Services
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local Workspace = game:GetService("Workspace")

--// Variables
local guiEnabled = false

--// Crear GUI principal
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "XollingHubGui"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game.CoreGui

-- Fondo principal negro semi-transparente
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.BorderSizePixel = 0
MainFrame.Size = UDim2.new(0, 450, 0, 350)
MainFrame.Position = UDim2.new(0.5, -225, 0.5, -175)
MainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
MainFrame.Parent = ScreenGui

-- Borde rojo intenso
local Border = Instance.new("UICorner")
Border.CornerRadius = UDim.new(0, 10)
Border.Parent = MainFrame

-- Logo "XH" (usando la ID proporcionada)
local Logo = Instance.new("ImageLabel")
Logo.Name = "Logo"
Logo.Size = UDim2.new(0, 60, 0, 60)
Logo.Position = UDim2.new(0, 15, 0, 15)
Logo.BackgroundTransparency = 1
Logo.Image = "rbxassetid://107228963378488"  -- Logo personalizado
Logo.Parent = MainFrame

-- Título
local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Text = "XollingHub"
Title.TextColor3 = Color3.fromRGB(220, 20, 20)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 28
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.BackgroundTransparency = 1
Title.Position = UDim2.new(0, 85, 0, 25)
Title.Size = UDim2.new(0, 200, 0, 35)
Title.Parent = MainFrame

-- Botón para cerrar GUI
local CloseBtn = Instance.new("TextButton")
CloseBtn.Name = "CloseBtn"
CloseBtn.Text = "X"
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.TextSize = 22
CloseBtn.TextColor3 = Color3.fromRGB(255, 60, 60)
CloseBtn.BackgroundTransparency = 1
CloseBtn.Position = UDim2.new(1, -40, 0, 15)
CloseBtn.Size = UDim2.new(0, 30, 0, 30)
CloseBtn.Parent = MainFrame
CloseBtn.MouseButton1Click:Connect(function()
    ScreenGui.Enabled = false
    guiEnabled = false
end)

-- Contenedor para pestañas
local TabContainer = Instance.new("Frame")
TabContainer.Name = "TabContainer"
TabContainer.Size = UDim2.new(1, -30, 1, -80)
TabContainer.Position = UDim2.new(0, 15, 0, 70)
TabContainer.BackgroundTransparency = 1
TabContainer.Parent = MainFrame

-- Crear sistema simple de pestañas

local Tabs = {}
local TabButtons = {}

local function createTab(name)
    -- Botón de pestaña
    local btn = Instance.new("TextButton")
    btn.Name = name.."Btn"
    btn.Text = name
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 18
    btn.TextColor3 = Color3.fromRGB(220, 20, 20)
    btn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    btn.Size = UDim2.new(0, 100, 0, 30)
    btn.Position = UDim2.new(0, (#TabButtons)*110, 0, 0)
    btn.Parent = MainFrame

    -- Contenido de la pestaña
    local frame = Instance.new("Frame")
    frame.Name = name.."Tab"
    frame.Size = UDim2.new(1, 0, 1, 0)
    frame.BackgroundTransparency = 1
    frame.Visible = false
    frame.Parent = TabContainer

    Tabs[name] = frame
    TabButtons[#TabButtons + 1] = btn

    btn.MouseButton1Click:Connect(function()
        for _, tab in pairs(Tabs) do
            tab.Visible = false
        end
        for _, b in pairs(TabButtons) do
            b.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
            b.TextColor3 = Color3.fromRGB(220, 20, 20)
        end
        frame.Visible = true
        btn.BackgroundColor3 = Color3.fromRGB(220, 20, 20)
        btn.TextColor3 = Color3.fromRGB(20, 20, 20)
    end)
end

-- Crear las pestañas que pediste
createTab("Main")
createTab("Duplicar")
createTab("Extras")

-- Activar la pestaña Main por defecto
TabButtons[1].MouseButton1Click:Wait()

-- === Contenido pestaña Main ===
do
    local mainTab = Tabs["Main"]

    local label = Instance.new("TextLabel")
    label.Text = "Bienvenido a XollingHub"
    label.TextColor3 = Color3.fromRGB(220, 20, 20)
    label.Font = Enum.Font.GothamBold
    label.TextSize = 20
    label.BackgroundTransparency = 1
    label.Size = UDim2.new(1, 0, 0, 30)
    label.Position = UDim2.new(0, 0, 0, 0)
    label.Parent = mainTab

    -- Aquí puedes agregar más controles para Main
end

-- === Contenido pestaña Duplicar ===
do
    local duplicarTab = Tabs["Duplicar"]

    local infoLabel = Instance.new("TextLabel")
    infoLabel.Text = "Duplica un objeto del Workspace"
    infoLabel.TextColor3 = Color3.fromRGB(220, 20, 20)
    infoLabel.Font = Enum.Font.Gotham
    infoLabel.TextSize = 18
    infoLabel.BackgroundTransparency = 1
    infoLabel.Size = UDim2.new(1, 0, 0, 25)
    infoLabel.Position = UDim2.new(0, 0, 0, 0)
    infoLabel.Parent = duplicarTab

    local inputBox = Instance.new("TextBox")
    inputBox.PlaceholderText = "Nombre del objeto a duplicar"
    inputBox.Text = ""
    inputBox.TextColor3 = Color3.fromRGB(255, 255, 255)
    inputBox.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    inputBox.Size = UDim2.new(1, 0, 0, 30)
    inputBox.Position = UDim2.new(0, 0, 0, 35)
    inputBox.ClearTextOnFocus = false
    inputBox.Parent = duplicarTab

    local dupBtn = Instance.new("TextButton")
    dupBtn.Text = "Duplicar"
    dupBtn.Font = Enum.Font.GothamBold
    dupBtn.TextSize = 20
    dupBtn.TextColor3 = Color3.fromRGB(20, 20, 20)
    dupBtn.BackgroundColor3 = Color3.fromRGB(220, 20, 20)
    dupBtn.Size = UDim2.new(0, 120, 0, 40)
    dupBtn.Position = UDim2.new(0, 0, 0, 75)
    dupBtn.Parent = duplicarTab

    dupBtn.MouseButton1Click:Connect(function()
        local objName = inputBox.Text
        if objName == "" then
            warn("Ingresa el nombre de un objeto válido.")
            return
        end

        local objetoOriginal = Workspace:FindFirstChild(objName)
        if objetoOriginal then
            local duplicado = objetoOriginal:Clone()
            duplicado.Parent = Workspace

            if duplicado:IsA("BasePart") then
                duplicado.Position = duplicado.Position + Vector3.new(5, 0, 0)
            elseif duplicado.PrimaryPart then
                duplicado:SetPrimaryPartCFrame(duplicado.PrimaryPart.CFrame * CFrame.new(5, 0, 0))
            end

            print("Objeto '" .. objName .. "' duplicado correctamente.")
        else
            warn("No se encontró el objeto '" .. objName .. "' en Workspace.")
        end
    end)
end

-- === Contenido pestaña Extras ===
do
    local extrasTab = Tabs["Extras"]

    local info = Instance.new("TextLabel")
    info.Text = "Aquí puedes agregar otras opciones."
    info.TextColor3 = Color3.fromRGB(220, 20, 20)
    info.Font = Enum.Font.Gotham
    info.TextSize = 18
    info.BackgroundTransparency = 1
    info.Size = UDim2.new(1, 0, 0, 30)
    info.Position = UDim2.new(0, 0, 0, 0)
    info.Parent = extrasTab

    -- Puedes añadir más botones o funciones aquí
end

-- Mostrar GUI
ScreenGui.Enabled = true
guiEnabled = true

-- Toggle con tecla RightControl para mostrar/ocultar GUI
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    if input.KeyCode == Enum.KeyCode.RightControl then
        guiEnabled = not guiEnabled
        ScreenGui.Enabled = guiEnabled
    end
end)

print("XollingHub cargado correctamente.")
