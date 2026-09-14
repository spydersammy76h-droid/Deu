# Deu
Ros
--// STEAL AN EGG - CUSTOM MENU
--// Versão para Roblox Studio
--// Um único LocalScript

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-------------------------------------------------------
-- CONFIG
-------------------------------------------------------

local GUI_NAME = "StealEggCustomMenu"

local Colors = {
    Background = Color3.fromRGB(8, 13, 25),
    Sidebar = Color3.fromRGB(11, 20, 36),
    Panel = Color3.fromRGB(16, 28, 48),
    Panel2 = Color3.fromRGB(22, 38, 63),
    Blue = Color3.fromRGB(0, 180, 255),
    Text = Color3.fromRGB(240, 245, 255),
    SubText = Color3.fromRGB(145, 160, 185),
    Off = Color3.fromRGB(65, 75, 90),
}

-------------------------------------------------------
-- LIMPAR GUI ANTIGA
-------------------------------------------------------

local old = playerGui:FindFirstChild(GUI_NAME)
if old then
    old:Destroy()
end

-------------------------------------------------------
-- FUNÇÕES
-------------------------------------------------------

local function Corner(obj, radius)
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, radius)
    c.Parent = obj
end

local function Stroke(obj)
    local s = Instance.new("UIStroke")
    s.Color = Color3.fromRGB(45, 75, 115)
    s.Transparency = 0.3
    s.Thickness = 1
    s.Parent = obj
end

local function Tween(obj, time, props)
    TweenService:Create(
        obj,
        TweenInfo.new(time, Enum.EasingStyle.Quart, Enum.EasingDirection.Out),
        props
    ):Play()
end

-------------------------------------------------------
-- GUI
-------------------------------------------------------

local gui = Instance.new("ScreenGui")
gui.Name = GUI_NAME
gui.ResetOnSpawn = false
gui.Parent = playerGui

-------------------------------------------------------
-- LOADING
-------------------------------------------------------

local loading = Instance.new("Frame")
loading.Size = UDim2.fromScale(1, 1)
loading.BackgroundColor3 = Colors.Background
loading.Parent = gui

local loadingTitle = Instance.new("TextLabel")
loadingTitle.Size = UDim2.new(1, 0, 0, 60)
loadingTitle.Position = UDim2.new(0, 0, .38, 0)
loadingTitle.BackgroundTransparency = 1
loadingTitle.Text = "STEAL AN EGG"
loadingTitle.TextColor3 = Colors.Blue
loadingTitle.Font = Enum.Font.GothamBold
loadingTitle.TextSize = 32
loadingTitle.Parent = loading

local loadingStatus = Instance.new("TextLabel")
loadingStatus.Size = UDim2.new(1, 0, 0, 30)
loadingStatus.Position = UDim2.new(0, 0, .47, 0)
loadingStatus.BackgroundTransparency = 1
loadingStatus.Text = "Carregando menu..."
loadingStatus.TextColor3 = Colors.SubText
loadingStatus.TextSize = 14
loadingStatus.Font = Enum.Font.Gotham
loadingStatus.Parent = loading

local barBack = Instance.new("Frame")
barBack.Size = UDim2.new(0, 360, 0, 10)
barBack.Position = UDim2.new(.5, -180, .54, 0)
barBack.BackgroundColor3 = Colors.Panel2
barBack.Parent = loading
Corner(barBack, 10)

local bar = Instance.new("Frame")
bar.Size = UDim2.new(0, 0, 1, 0)
bar.BackgroundColor3 = Colors.Blue
bar.Parent = barBack
Corner(bar, 10)

Tween(bar, 2, {
    Size = UDim2.new(1, 0, 1, 0)
})

task.wait(2.1)

Tween(loading, .3, {
    BackgroundTransparency = 1
})

task.wait(.35)
loading:Destroy()

-------------------------------------------------------
-- JANELA
-------------------------------------------------------

local window = Instance.new("Frame")
window.Size = UDim2.new(0, 720, 0, 470)
window.Position = UDim2.new(.5, -360, .5, -235)
window.BackgroundColor3 = Colors.Background
window.Parent = gui

Corner(window, 14)
Stroke(window)

-------------------------------------------------------
-- HEADER
-------------------------------------------------------

local header = Instance.new("Frame")
header.Size = UDim2.new(1, 0, 0, 60)
header.BackgroundColor3 = Colors.Panel
header.Parent = window
Corner(header, 14)

local logo = Instance.new("TextLabel")
logo.Size = UDim2.new(0, 120, 1, 0)
logo.Position = UDim2.new(0, 18, 0, 0)
logo.BackgroundTransparency = 1
logo.Text = "ZN"
logo.TextColor3 = Colors.Blue
logo.TextSize = 27
logo.Font = Enum.Font.GothamBold
logo.TextXAlignment = Enum.TextXAlignment.Left
logo.Parent = header

local status = Instance.new("TextLabel")
status.Size = UDim2.new(0, 150, 1, 0)
status.Position = UDim2.new(1, -205, 0, 0)
status.BackgroundTransparency = 1
status.Text = "● Studio"
status.TextColor3 = Colors.SubText
status.TextSize = 13
status.Font = Enum.Font.Gotham
status.Parent = header

local close = Instance.new("TextButton")
close.Size = UDim2.new(0, 40, 0, 40)
close.Position = UDim2.new(1, -45, 0, 10)
close.BackgroundTransparency = 1
close.Text = "×"
close.TextColor3 = Colors.Text
close.TextSize = 28
close.Font = Enum.Font.Gotham
close.Parent = header

close.MouseButton1Click:Connect(function()
    Tween(window, .25, {
        Size = UDim2.new(0, 0, 0, 0)
    })

    task.wait(.3)
    gui:Destroy()
end)

-------------------------------------------------------
-- SIDEBAR
-------------------------------------------------------

local sidebar = Instance.new("Frame")
sidebar.Size = UDim2.new(0, 195, 1, -60)
sidebar.Position = UDim2.new(0, 0, 0, 60)
sidebar.BackgroundColor3 = Colors.Sidebar
sidebar.Parent = window

local search = Instance.new("TextBox")
search.Size = UDim2.new(1, -24, 0, 38)
search.Position = UDim2.new(0, 12, 0, 15)
search.BackgroundColor3 = Colors.Panel2
search.PlaceholderText = "⌕  Search..."
search.PlaceholderColor3 = Colors.SubText
search.TextColor3 = Colors.Text
search.Text = ""
search.TextSize = 13
search.Font = Enum.Font.Gotham
search.Parent = sidebar
Corner(search, 8)

-------------------------------------------------------
-- ÁREA DE PÁGINAS
-------------------------------------------------------

local content = Instance.new("Frame")
content.Size = UDim2.new(1, -210, 1, -80)
content.Position = UDim2.new(0, 205, 0, 70)
content.BackgroundTransparency = 1
content.Parent = window

local pages = {}

local function NewPage(name)
    local page = Instance.new("ScrollingFrame")
    page.Name = name
    page.Size = UDim2.fromScale(1, 1)
    page.BackgroundTransparency = 1
    page.BorderSizePixel = 0
    page.ScrollBarThickness = 3
    page.CanvasSize = UDim2.new(0, 0, 0, 600)
    page.Visible = false
    page.Parent = content

    pages[name] = page
    return page
end

local Main = NewPage("Main")
local Event = NewPage("Event")
local Spawn = NewPage("Spawn")
local Farm = NewPage("Farm")
local Player = NewPage("Player")
local Settings = NewPage("Settings")

-------------------------------------------------------
-- TÍTULO
-------------------------------------------------------

local function PageTitle(page, title, description)

    local t = Instance.new("TextLabel")
    t.Size = UDim2.new(1, -10, 0, 40)
    t.BackgroundTransparency = 1
    t.Text = title
    t.TextColor3 = Colors.Text
    t.TextSize = 23
    t.Font = Enum.Font.GothamBold
    t.TextXAlignment = Enum.TextXAlignment.Left
    t.Parent = page

    local d = Instance.new("TextLabel")
    d.Size = UDim2.new(1, -10, 0, 25)
    d.Position = UDim2.new(0, 0, 0, 38)
    d.BackgroundTransparency = 1
    d.Text = description
    d.TextColor3 = Colors.SubText
    d.TextSize = 12
    d.Font = Enum.Font.Gotham
    d.TextXAlignment = Enum.TextXAlignment.Left
    d.Parent = page
end

PageTitle(Main, "Auto Farm", "Funções do seu jogo")
PageTitle(Event, "Event", "Eventos disponíveis")
PageTitle(Spawn, "Egg Spawn", "Gerenciamento dos ovos")
PageTitle(Farm, "Farm", "Automação")
PageTitle(Player, "Player", "Configurações do jogador")
PageTitle(Settings, "Configurações", "Configurações do menu")

-------------------------------------------------------
-- TOGGLE
-------------------------------------------------------

local function Toggle(page, text, y, callback)

    local row = Instance.new("Frame")
    row.Size = UDim2.new(1, -15, 0, 48)
    row.Position = UDim2.new(0, 0, 0, y)
    row.BackgroundTransparency = 1
    row.Parent = page

    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, -70, 1, 0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Colors.Text
    label.TextSize = 14
    label.Font = Enum.Font.Gotham
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = row

    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 43, 0, 23)
    button.Position = UDim2.new(1, -48, .5, -11)
    button.BackgroundColor3 = Colors.Off
    button.Text = ""
    button.Parent = row
    Corner(button, 20)

    local circle = Instance.new("Frame")
    circle.Size = UDim2.new(0, 17, 0, 17)
    circle.Position = UDim2.new(0, 3, .5, -8)
    circle.BackgroundColor3 = Color3.new(1, 1, 1)
    circle.Parent = button
    Corner(circle, 20)

    local active = false

    button.MouseButton1Click:Connect(function()

        active = not active

        if active then
            Tween(button, .18, {
                BackgroundColor3 = Colors.Blue
            })

            Tween(circle, .18, {
                Position = UDim2.new(1, -20, .5, -8)
            })
        else
            Tween(button, .18, {
                BackgroundColor3 = Colors.Off
            })

            Tween(circle, .18, {
                Position = UDim2.new(0, 3, .5, -8)
            })
        end

        if callback then
            callback(active)
        end
    end)
end

-------------------------------------------------------
-- BOTÃO
-------------------------------------------------------

local function Button(page, text, y, callback)

    local b = Instance.new("TextButton")
    b.Size = UDim2.new(1, -15, 0, 45)
    b.Position = UDim2.new(0, 0, 0, y)
    b.BackgroundColor3 = Colors.Panel2
    b.Text = text
    b.TextColor3 = Colors.Text
    b.TextSize = 14
    b.Font = Enum.Font.GothamBold
    b.Parent = page
    Corner(b, 8)

    b.MouseButton1Click:Connect(function()
        if callback then
            callback()
        end
    end)

    return b
end

-------------------------------------------------------
-- MAIN
-------------------------------------------------------

Toggle(Main, "Auto Steal", 80, function(v)
    print("Auto Steal:", v)
end)

Toggle(Main, "Auto Treadmill", 135, function(v)
    print("Auto Treadmill:", v)
end)

Toggle(Main, "Anti Knock Back", 190, function(v)
    print("Anti Knock Back:", v)
end)

-------------------------------------------------------
-- SPAWN
-------------------------------------------------------

Button(Spawn, "🥚 Spawnar Ovo Comum", 80, function()

    local character = player.Character
    if not character then return end

    local root = character:FindFirstChild("HumanoidRootPart")
    if not root then return end

    local egg = Instance.new("Part")
    egg.Name = "Egg_Comum"
    egg.Shape = Enum.PartType.Ball
    egg.Size = Vector3.new(3, 3, 3)
    egg.Anchored = true
    egg.Position = root.Position + root.CFrame.LookVector * 7
    egg.Parent = workspace

    print("Ovo comum criado")
end)

Button(Spawn, "✨ Spawnar Ovo Raro", 135, function()

    local character = player.Character
    if not character then return end

    local root = character:FindFirstChild("HumanoidRootPart")
    if not root then return end

    local egg = Instance.new("Part")
    egg.Name = "Egg_Raro"
    egg.Shape = Enum.PartType.Ball
    egg.Size = Vector3.new(3.5, 3.5, 3.5)
    egg.Anchored = true
    egg.Position = root.Position + root.CFrame.LookVector * 7
    egg.Parent = workspace

    print("Ovo raro criado")
end)

Button(Spawn, "👑 Spawnar Ovo Lendário", 190, function()

    local character = player.Character
    if not character then return end

    local root = character:FindFirstChild("HumanoidRootPart")
    if not root then return end

    local egg = Instance.new("Part")
    egg.Name = "Egg_Lendario"
    egg.Shape = Enum.PartType.Ball
    egg.Size = Vector3.new(4, 4, 4)
    egg.Anchored = true
    egg.Position = root.Position + root.CFrame.LookVector * 7
    egg.Parent = workspace

    print("Ovo lendário criado")
end)

-------------------------------------------------------
-- FARM
-------------------------------------------------------

Toggle(Farm, "Auto Coletar", 80, function(v)
    print("Auto Coletar:", v)
end)

Toggle(Farm, "Auto Abrir Ovos", 135, function(v)
    print("Auto Abrir:", v)
end)

Toggle(Farm, "Auto Vender", 190, function(v)
    print("Auto Vender:", v)
end)

-------------------------------------------------------
-- EVENT
-------------------------------------------------------

Toggle(Event, "Evento Ativo", 80, function(v)
    print("Evento:", v)
end)

Button(Event, "🎁 Abrir painel de eventos", 140, function()
    print("Painel de eventos aberto")
end)

-------------------------------------------------------
-- PLAYER
-------------------------------------------------------

Toggle(Player, "Modo de velocidade", 80, function(v)
    print("Velocidade:", v)
end)

-------------------------------------------------------
-- CONFIGURAÇÕES
-------------------------------------------------------

Toggle(Settings, "Animações", 80, function(v)
    print("Animações:", v)
end)

Toggle(Settings, "Som", 135, function(v)
    print("Som:", v)
end)

-------------------------------------------------------
-- TABS
-------------------------------------------------------

local tabData = {
    {"⌂", "Main", Main},
    {"✦", "Event", Event},
    {"🥚", "Spawn", Spawn},
    {"↻", "Farm", Farm},
    {"●", "Player", Player},
    {"⚙", "Config", Settings},
}

local selected

for i, data in ipairs(tabData) do

    local icon = data[1]
    local name = data[2]
    local page = data[3]

    local tab = Instance.new("TextButton")
    tab.Size = UDim2.new(1, -18, 0, 43)
    tab.Position = UDim2.new(0, 9, 0, 65 + (i - 1) * 48)
    tab.BackgroundColor3 = Colors.Sidebar
    tab.Text = icon .. "   " .. name
    tab.TextColor3 = Colors.SubText
    tab.TextSize = 14
    tab.Font = Enum.Font.GothamBold
    tab.TextXAlignment = Enum.TextXAlignment.Left
    tab.Parent = sidebar
    Corner(tab, 7)

    tab.MouseButton1Click:Connect(function()

        for _, p in pairs(pages) do
            p.Visible = false
        end

        page.Visible = true

        if selected then
            selected.BackgroundColor3 = Colors.Sidebar
            selected.TextColor3 = Colors.SubText
        end

        selected = tab

        tab.BackgroundColor3 = Colors.Blue
        tab.TextColor3 = Color3.new(1, 1, 1)

        page.Position = UDim2.new(0, 25, 0, 0)

        Tween(page, .2, {
            Position = UDim2.new(0, 0, 0, 0)
        })
    end)
end

-------------------------------------------------------
-- PÁGINA INICIAL
-------------------------------------------------------

Main.Visible = true

-------------------------------------------------------
-- ANIMAÇÃO DA JANELA
-------------------------------------------------------

window.Size = UDim2.new(0, 0, 0, 0)

Tween(window, .45, {
    Size = UDim2.new(0, 720, 0, 470)
})

print("Steal An Egg Menu carregado!")
