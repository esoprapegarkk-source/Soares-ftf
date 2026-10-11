
-- SOARES FTF | FLEE FACILITY
-- Menu preto compacto; sem Shift Lock e sem ESP da Beast
-- LocalScript em StarterPlayer > StarterPlayerScripts

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local ICON_ID = "rbxassetid://100427330095686"

-- LIMPAR INTERFACES ANTIGAS
for _, name in ipairs({"SoaresFTFLoading", "SoaresFTF"}) do
    local old = playerGui:FindFirstChild(name)
    if old then old:Destroy() end
end

-- ANIMAÇÃO DE CARREGAMENTO
local loadingGui = Instance.new("ScreenGui")
loadingGui.Name = "SoaresFTFLoading"
loadingGui.IgnoreGuiInset = true
loadingGui.DisplayOrder = 999
loadingGui.ResetOnSpawn = false
loadingGui.Parent = playerGui

local bg = Instance.new("Frame")
bg.Size = UDim2.fromScale(1, 1)
bg.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
bg.BorderSizePixel = 0
bg.Parent = loadingGui

local loadingTitle = Instance.new("TextLabel")
loadingTitle.Size = UDim2.new(1, 0, 0, 65)
loadingTitle.Position = UDim2.new(0, 0, 0.36, 0)
loadingTitle.BackgroundTransparency = 1
loadingTitle.Text = "SOARES FTF"
loadingTitle.TextColor3 = Color3.fromRGB(220, 25, 40)
loadingTitle.Font = Enum.Font.GothamBlack
loadingTitle.TextScaled = true
loadingTitle.Parent = bg

local titleLimit = Instance.new("UITextSizeConstraint")
titleLimit.MaxTextSize = 48
titleLimit.MinTextSize = 20
titleLimit.Parent = loadingTitle

local subtitleLoad = Instance.new("TextLabel")
subtitleLoad.Size = UDim2.new(1, 0, 0, 30)
subtitleLoad.Position = UDim2.new(0, 0, 0.48, 0)
subtitleLoad.BackgroundTransparency = 1
subtitleLoad.Text = "INICIANDO..."
subtitleLoad.TextColor3 = Color3.fromRGB(200, 200, 200)
subtitleLoad.Font = Enum.Font.GothamBold
subtitleLoad.TextSize = 14
subtitleLoad.Parent = bg

local barBack = Instance.new("Frame")
barBack.Size = UDim2.new(0.65, 0, 0, 8)
barBack.Position = UDim2.new(0.175, 0, 0.56, 0)
barBack.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
barBack.BorderSizePixel = 0
barBack.ClipsDescendants = true
barBack.Parent = bg

local barCorner = Instance.new("UICorner")
barCorner.CornerRadius = UDim.new(1, 0)
barCorner.Parent = barBack

local barFill = Instance.new("Frame")
barFill.Size = UDim2.new(0, 0, 1, 0)
barFill.BackgroundColor3 = Color3.fromRGB(220, 25, 40)
barFill.BorderSizePixel = 0
barFill.Parent = barBack

local fillCorner = Instance.new("UICorner")
fillCorner.CornerRadius = UDim.new(1, 0)
fillCorner.Parent = barFill

local percent = Instance.new("TextLabel")
percent.Size = UDim2.new(1, 0, 0, 25)
percent.Position = UDim2.new(0, 0, 0.59, 0)
percent.BackgroundTransparency = 1
percent.Text = "0%"
percent.TextColor3 = Color3.new(1, 1, 1)
percent.Font = Enum.Font.GothamBold
percent.TextSize = 13
percent.Parent = bg

local pulse = TweenService:Create(
    loadingTitle,
    TweenInfo.new(0.7, Enum.EasingStyle.Sine,
        Enum.EasingDirection.InOut, -1, true),
    {TextColor3 = Color3.fromRGB(255, 100, 100)}
)
pulse:Play()

for i = 1, 100 do
    percent.Text = i .. "%"

    if i < 35 then
        subtitleLoad.Text = "CARREGANDO INTERFACE..."
    elseif i < 70 then
        subtitleLoad.Text = "PREPARANDO SOARES FTF..."
    else
        subtitleLoad.Text = "FINALIZANDO..."
    end

    barFill.Size = UDim2.new(i / 100, 0, 1, 0)
    task.wait(0.025)
end

subtitleLoad.Text = "PRONTO!"
task.wait(0.4)
pulse:Cancel()

local fade = TweenInfo.new(0.5)
TweenService:Create(bg, fade, {BackgroundTransparency = 1}):Play()
TweenService:Create(loadingTitle, fade, {TextTransparency = 1}):Play()
TweenService:Create(subtitleLoad, fade, {TextTransparency = 1}):Play()
TweenService:Create(barBack, fade, {BackgroundTransparency = 1}):Play()
TweenService:Create(barFill, fade, {BackgroundTransparency = 1}):Play()
TweenService:Create(percent, fade, {TextTransparency = 1}):Play()

task.wait(0.6)
loadingGui:Destroy()

-- MENU SOARES FTF
local gui = Instance.new("ScreenGui")
gui.Name = "SoaresFTF"
gui.ResetOnSpawn = false
gui.DisplayOrder = 100
gui.Parent = playerGui

-- PAINEL PRINCIPAL PRETO E COMPACTO
local main = Instance.new("Frame")
main.Name = "MainPanel"
main.Size = UDim2.fromOffset(220, 320)
main.Position = UDim2.new(0, 10, 0.25, 0)
main.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
main.BorderSizePixel = 0
main.Active = true
main.Parent = gui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 12)
corner.Parent = main

local stroke = Instance.new("UIStroke")
stroke.Color = Color3.fromRGB(95, 95, 95)
stroke.Thickness = 1.5
stroke.Parent = main

-- TÍTULO
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -55, 0, 40)
title.Position = UDim2.fromOffset(8, 5)
title.BackgroundTransparency = 1
title.Text = "SOARES FTF"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.GothamBlack
title.TextSize = 19
title.TextXAlignment = Enum.TextXAlignment.Left
title.Active = true
title.Parent = main

-- BOTÃO MINIMIZAR
local minimize = Instance.new("TextButton")
minimize.Name = "MinimizeButton"
minimize.Size = UDim2.fromOffset(28, 28)
minimize.Position = UDim2.new(1, -35, 0, 7)
minimize.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
minimize.Text = "X"
minimize.TextColor3 = Color3.new(1, 1, 1)
minimize.Font = Enum.Font.GothamBlack
minimize.TextSize = 14
minimize.Parent = main

local minCorner = Instance.new("UICorner")
minCorner.CornerRadius = UDim.new(0, 8)
minCorner.Parent = minimize

-- ÍCONE FLUTUANTE MENOR
local iconButton = Instance.new("ImageButton")
iconButton.Name = "FloatingIcon"
iconButton.Size = UDim2.fromOffset(45, 45)
iconButton.Position = UDim2.new(0, 10, 0.45, 0)
iconButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
iconButton.Image = ICON_ID
iconButton.ScaleType = Enum.ScaleType.Crop
iconButton.Visible = false
iconButton.Active = true
iconButton.Parent = gui

local iconCorner = Instance.new("UICorner")
iconCorner.CornerRadius = UDim.new(1, 0)
iconCorner.Parent = iconButton

local iconStroke = Instance.new("UIStroke")
iconStroke.Color = Color3.fromRGB(180, 180, 180)
iconStroke.Thickness = 2
iconStroke.Parent = iconButton

-- ARRASTAR PAINEL E ÍCONE
local dragObject, dragStart, startPosition
local activeTouch, moved, suppressClick

local function beginDrag(object, input)
    if input.UserInputType ~= Enum.UserInputType.MouseButton1
        and input.UserInputType ~= Enum.UserInputType.Touch then
        return
    end

    dragObject = object
    dragStart = input.Position
    startPosition = object.Position
    activeTouch = input.UserInputType == Enum.UserInputType.Touch
        and input or nil
    moved = false
end

title.InputBegan:Connect(function(input)
    beginDrag(main, input)
end)

main.InputBegan:Connect(function(input)
    beginDrag(main, input)
end)

iconButton.InputBegan:Connect(function(input)
    beginDrag(iconButton, input)
end)

UIS.InputChanged:Connect(function(input)
    if not dragObject then return end

    local isMouse = input.UserInputType == Enum.UserInputType.MouseMovement
    local isTouch = activeTouch ~= nil and input == activeTouch
    if not isMouse and not isTouch then return end

    local delta = input.Position - dragStart
    if math.abs(delta.X) > 5 or math.abs(delta.Y) > 5 then
        moved = true
    end

    dragObject.Position = UDim2.new(
        startPosition.X.Scale,
        startPosition.X.Offset + delta.X,
        startPosition.Y.Scale,
        startPosition.Y.Offset + delta.Y
    )
end)

UIS.InputEnded:Connect(function(input)
    if not dragObject then return end

    if input.UserInputType == Enum.UserInputType.MouseButton1
        or input.UserInputType == Enum.UserInputType.Touch then

        if moved and dragObject == iconButton then
            suppressClick = true
        end

        dragObject = nil
        dragStart = nil
        startPosition = nil
        activeTouch = nil
        moved = false
    end
end)

minimize.Activated:Connect(function()
    main.Visible = false
    iconButton.Visible = true
end)

iconButton.Activated:Connect(function()
    if suppressClick then
        suppressClick = false
        return
    end

    main.Visible = true
    iconButton.Visible = false
end)

-- SUBTÍTULO
local subtitle = Instance.new("TextLabel")
subtitle.Size = UDim2.new(1, 0, 0, 18)
subtitle.Position = UDim2.fromOffset(0, 39)
subtitle.BackgroundTransparency = 1
subtitle.Text = "SOARES FTF"
subtitle.TextColor3 = Color3.fromRGB(160, 160, 160)
subtitle.Font = Enum.Font.Gotham
subtitle.TextSize = 9
subtitle.Parent = main

-- ÁREA DOS BOTÕES
local container = Instance.new("ScrollingFrame")
container.Name = "ButtonsContainer"
container.Size = UDim2.new(1, -20, 1, -72)
container.Position = UDim2.fromOffset(10, 65)
container.BackgroundTransparency = 1
container.BorderSizePixel = 0
container.ScrollBarThickness = 3
container.AutomaticCanvasSize = Enum.AutomaticSize.Y
container.CanvasSize = UDim2.new(0, 0, 0, 0)
container.Parent = main

local layout = Instance.new("UIListLayout")
layout.Padding = UDim.new(0, 6)
layout.SortOrder = Enum.SortOrder.LayoutOrder
layout.Parent = container

local enabled = {}

local function makeButton(name, callback)
    local button = Instance.new("TextButton")
    button.Name = name
    button.Size = UDim2.new(1, -5, 0, 34)
    button.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    button.TextColor3 = Color3.new(1, 1, 1)
    button.Font = Enum.Font.GothamBold
    button.TextSize = 11
    button.Text = name .. " [OFF]"
    button.Parent = container

    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 7)
    c.Parent = button

    enabled[name] = false

    button.Activated:Connect(function()
        enabled[name] = not enabled[name]
        local on = enabled[name]

        button.Text = name .. (on and " [ON]" or " [OFF]")
        button.BackgroundColor3 = on
            and Color3.fromRGB(75, 20, 30)
            or Color3.fromRGB(0, 0, 0)

        if callback then callback(on) end
    end)

    return button
end

-- CORES: ESP PESSOAS E COMPUTADORES
local colorOptions = {
    {name = "Vermelho", color = Color3.fromRGB(255, 0, 0)},
    {name = "Azul", color = Color3.fromRGB(0, 120, 255)},
    {name = "Verde", color = Color3.fromRGB(0, 255, 100)},
    {name = "Roxo", color = Color3.fromRGB(180, 0, 255)},
    {name = "Amarelo", color = Color3.fromRGB(255, 220, 0)},
    {name = "Rosa", color = Color3.fromRGB(255, 60, 170)},
    {name = "Ciano", color = Color3.fromRGB(0, 220, 255)},
    {name = "Branco", color = Color3.fromRGB(255, 255, 255)},
    {name = "Verde-claro", color = Color3.fromRGB(144, 238, 144)}
}

local playerColorIndex = 1
local computerColorIndex = 7
local playerESPColor = colorOptions[playerColorIndex].color
local computerESPColor = colorOptions[computerColorIndex].color

local highlights = {}
local characterConnections = {}

-- ESP PESSOAS: SEM ESP DA BEAST
local function removeESP(target)
    if highlights[target] then
        highlights[target]:Destroy()
        highlights[target] = nil
    end
end

local function addESP(target)
    if target == player then return end

    if not enabled["ESP Pessoas"] then
        removeESP(target)
        return
    end

    local character = target.Character
    if not character then return end

    removeESP(target)

    local h = Instance.new("Highlight")
    h.Name = "SoaresPlayerESP"
    h.FillColor = playerESPColor
    h.OutlineColor = Color3.new(1, 1, 1)
    h.FillTransparency = 0.35
    h.OutlineTransparency = 0
    h.Adornee = character
    h.Parent = character

    highlights[target] = h
end

local function watchPlayer(target)
    if target == player or characterConnections[target] then return end

    characterConnections[target] = target.CharacterAdded:Connect(function()
        task.wait(1)
        addESP(target)
    end)

    if enabled["ESP Pessoas"] then
        addESP(target)
    end
end

local function updateESP(on)
    for _, target in ipairs(Players:GetPlayers()) do
        if on then
            watchPlayer(target)
            addESP(target)
        else
            removeESP(target)
        end
    end
end

makeButton("ESP Pessoas", updateESP)

-- ESP COMPUTADORES
local computerHighlights = {}

local function clearComputerESP()
    for object, highlight in pairs(computerHighlights) do
        highlight:Destroy()
        computerHighlights[object] = nil
    end
end

local function scanComputers()
    clearComputerESP()
    if not enabled["ESP Computadores"] then return end

    for _, object in ipairs(workspace:GetDescendants()) do
        local name = string.lower(object.Name)
        local matches = name:find("computer", 1, true)
            or name:find("computador", 1, true)
            or name == "pc"

        if matches and (object:IsA("Model") or object:IsA("BasePart")) then
            local parent = object.Parent
            local insideComputerModel = false

            while parent and parent ~= workspace do
                local parentName = string.lower(parent.Name)

                if parent:IsA("Model") and (
                    parentName:find("computer", 1, true)
                    or parentName:find("computador", 1, true)
                    or parentName == "pc"
                ) then
                    insideComputerModel = true
                    break
                end

                parent = parent.Parent
            end

            if not insideComputerModel then
                local h = Instance.new("Highlight")
                h.Name = "SoaresComputerESP"
                h.FillColor = computerESPColor
                h.OutlineColor = Color3.new(1, 1, 1)
                h.FillTransparency = 0.4
                h.Adornee = object
                h.Parent = object
                computerHighlights[object] = h
            end
        end
    end
end

makeButton("ESP Computadores", function(on)
    if on then
        scanComputers()
    else
        clearComputerESP()
    end
end)

-- SELETORES DE COR
local function makeColorButton(label, getIndex, setIndex, applyColor)
    local button = Instance.new("TextButton")
    button.Name = label
    button.Size = UDim2.new(1, -5, 0, 34)
    button.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    button.TextColor3 = Color3.new(1, 1, 1)
    button.Font = Enum.Font.GothamBold
    button.TextSize = 10
    button.Parent = container

    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 7)
    c.Parent = button

    local function refresh()
        local option = colorOptions[getIndex()]
        button.Text = label .. ": " .. option.name
        button.BackgroundColor3 = option.color
    end

    button.Activated:Connect(function()
        local nextIndex = getIndex() % #colorOptions + 1
        setIndex(nextIndex)
        applyColor(colorOptions[nextIndex].color)
        refresh()
    end)

    refresh()
end

local function changePlayerColor(color)
    playerESPColor = color

    for _, h in pairs(highlights) do
        if h and h.Parent then
            h.FillColor = color
        end
    end
end

local function changeComputerColor(color)
    computerESPColor = color

    for _, h in pairs(computerHighlights) do
        if h and h.Parent then
            h.FillColor = color
        end
    end
end

makeColorButton(
    "Cor dos Players",
    function() return playerColorIndex end,
    function(i) playerColorIndex = i end,
    changePlayerColor
)

makeColorButton(
    "Cor dos Computadores",
    function() return computerColorIndex end,
    function(i) computerColorIndex = i end,
    changeComputerColor
)

-- REFRESH ESP
makeButton("Refresh ESP", function()
    for _, target in ipairs(Players:GetPlayers()) do
        removeESP(target)
    end

    if enabled["ESP Pessoas"] then
        for _, target in ipairs(Players:GetPlayers()) do
            addESP(target)
        end
    end

    scanComputers()
    print("SOARES FTF: ESP atualizado!")
end)

Players.PlayerAdded:Connect(watchPlayer)

Players.PlayerRemoving:Connect(function(target)
    removeESP(target)

    if characterConnections[target] then
        characterConnections[target]:Disconnect()
        characterConnections[target] = nil
    end
end)

for _, target in ipairs(Players:GetPlayers()) do
    watchPlayer(target)
end

-- PULO INFINITO
local jumpConnection

makeButton("Infinite Jump", function(on)
    if jumpConnection then
        jumpConnection:Disconnect()
        jumpConnection = nil
    end

    if on then
        jumpConnection = UIS.JumpRequest:Connect(function()
            local character = player.Character
            local humanoid = character
                and character:FindFirstChildOfClass("Humanoid")

            if humanoid and humanoid.Health > 0 then
                humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
            end
        end)
    end
end)

-- SPRINT
local function applySpeed(on)
    local character = player.Character
    local humanoid = character
        and character:FindFirstChildOfClass("Humanoid")

    if humanoid then
        humanoid.WalkSpeed = on and 26 or 16
    end
end

makeButton("Sprint", applySpeed)

-- RESTAURAR VELOCIDADE AO RENASCER
player.CharacterAdded:Connect(function()
    task.wait(0.5)
    applySpeed(enabled["Sprint"] or false)

    if enabled["ESP Pessoas"] then
        for _, target in ipairs(Players:GetPlayers()) do
            addESP(target)
        end
    end
end)

-- MOSTRAR MENU
main.Visible = true
iconButton.Visible = false

print("SOARES FTF carregado!")
