local Player = game.Players.LocalPlayer
local Char = Player.Character or Player.CharacterAdded:Wait()
local RootPart = Char:WaitForChild("HumanoidRootPart")
local humanoid = Char:WaitForChild("Humanoid")
local flying, bodyVelocity, speed = false, nil, 50
local shiftLock = false

-- Функция для включения/выключения полета
local function toggleFly()
    if flying then
        flying = false
        if bodyVelocity then bodyVelocity:Destroy() end
    else
        flying = true
        bodyVelocity = Instance.new("BodyVelocity")
        bodyVelocity.MaxForce = Vector3.new(400000, 400000, 400000)
        bodyVelocity.Parent = RootPart
    end
end

-- Функция для включения/выключения shift lock
local function toggleShiftLock()
    shiftLock = not shiftLock
    if shiftLock then
        humanoid.PlatformStand = true
        Player.DevComputerMovementMode = Enum.DevComputerMovementMode.Scriptable
    else
        humanoid.PlatformStand = false
        Player.DevComputerMovementMode = Enum.DevComputerMovementMode.UserSwitch
    end
end

-- Создание UI для кнопок
local ScreenGui = Instance.new("ScreenGui", Player:WaitForChild("PlayerGui"))
local mainButton = Instance.new("TextButton", ScreenGui)
mainButton.Size = UDim2.new(0, 40, 0, 40)
mainButton.Position = UDim2.new(0.8, -40, 0.9, -40)
mainButton.Text = "☰"
mainButton.TextSize = 20
mainButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
mainButton.TextColor3 = Color3.fromRGB(255, 255, 255)
mainButton.Draggable = true

-- Контейнер для меню
local menuOpen = false
local menuFrame = Instance.new("Frame", ScreenGui)
menuFrame.Size = UDim2.new(0, 250, 0, 200)
menuFrame.Position = UDim2.new(0.5, -125, 0.5, -100)
menuFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
menuFrame.Visible = false

-- Заголовок меню
local titleLabel = Instance.new("TextLabel", menuFrame)
titleLabel.Size = UDim2.new(1, 0, 0.2, 0)
titleLabel.Position = UDim2.new(0, 0, 0, 0)
titleLabel.Text = "t/me:CellDelta-Scripts"
titleLabel.TextSize = 20
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
titleLabel.TextScaled = true

-- Кнопка для полета
local flyButton = Instance.new("TextButton", menuFrame)
flyButton.Size = UDim2.new(0, 200, 0, 50)
flyButton.Position = UDim2.new(0.5, -100, 0.3, 0)
flyButton.Text = "Fly: OFF"

-- Кнопка для shift lock
local shiftLockButton = Instance.new("TextButton", menuFrame)
shiftLockButton.Size = UDim2.new(0, 200, 0, 50)
shiftLockButton.Position = UDim2.new(0.5, -100, 0.5, 0)
shiftLockButton.Text = "ShiftLock: OFF"

-- Кнопка для закрытия меню
local closeButton = Instance.new("TextButton", menuFrame)
closeButton.Size = UDim2.new(0, 30, 0, 30)
closeButton.Position = UDim2.new(0.5, -15, 0, -50)
closeButton.Text = "X"
closeButton.TextSize = 20
closeButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

-- Открытие/закрытие меню
mainButton.MouseButton1Click:Connect(function()
    menuOpen = not menuOpen
    menuFrame.Visible = menuOpen
end)

-- Закрытие меню
closeButton.MouseButton1Click:Connect(function()
    menuOpen = false
    menuFrame.Visible = false
end)

-- Включение/выключение полета
flyButton.MouseButton1Click:Connect(function()
    toggleFly()
    flyButton.Text = flying and "Fly: ON" or "Fly: OFF"
end)

-- Включение/выключение shift lock
shiftLockButton.MouseButton1Click:Connect(function()
    toggleShiftLock()
    shiftLockButton.Text = shiftLock and "ShiftLock: ON" or "ShiftLock: OFF"
end)

-- Обработка полета при каждом кадре
game:GetService("RunService").Heartbeat:Connect(function()
    if flying then
        local camera = game.Workspace.CurrentCamera
        local lookAtPosition = camera.CFrame.p + (camera.CFrame.LookVector * 100)
        local directionToTarget = (lookAtPosition - RootPart.Position).unit
        bodyVelocity.Velocity = directionToTarget * speed
    end
end)
