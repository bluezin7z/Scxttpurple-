-- Configurações
local velocidadeMaxima = 150
local alturaSalto = 150

-- Serviços
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

-- Variáveis
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")

-- Função para alterar velocidade
local function setVelocidade(velocidade)
    if humanoid then
        humanoid.WalkSpeed = velocidade
    end
end

-- Função para salto automático
local function saltoAuto()
    if humanoid then
        humanoid.JumpPower = alturaSalto
        humanoid.Jump = true
    end
end

-- Eventos
UserInputService.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.LeftShift then
        setVelocidade(velocidadeMaxima)
    elseif input.KeyCode == Enum.KeyCode.Space then
        saltoAuto()
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.LeftShift then
        setVelocidade(16) -- Velocidade padrão
    end
end)

-- Loop para manter a velocidade
RunService.RenderStepped:Connect(function()
    if humanoid and humanoid.WalkSpeed > 16 then
        setVelocidade(velocidadeMaxima)
    end
end)
