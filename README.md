# (🟢) Remove completamente a skin dos jogadores.
```
local function removerAcessoriosEPele(personagem)
    for _, acessorio in pairs(personagem:GetChildren()) do
        if acessorio:IsA("Accessory") then
            acessorio:Destroy()
        end
    end
    for _, item in pairs(personagem:GetChildren()) do
        if item:IsA("Clothing") or item:IsA("ShirtGraphic") then
            item:Destroy()
        end
    end
    for _, parte in pairs(personagem:GetChildren()) do
        if parte:IsA("BasePart") and parte.Name ~= "HumanoidRootPart" then
            parte.Color = Color3.new(1, 1, 1)
        end
    end
end

local function aplicarParaJogador(jogador)
    jogador.CharacterAdded:Connect(function(personagem)
        removerAcessoriosEPele(personagem)
    end)
    if jogador.Character then
        removerAcessoriosEPele(jogador.Character)
    end
end

local function aplicarParaTodos()
    for _, jogador in pairs(game.Players:GetPlayers()) do
        aplicarParaJogador(jogador)
    end
end

game.Players.PlayerAdded:Connect(aplicarParaJogador)

aplicarParaTodos()
