local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/kwargs_Ui_Library/main/source.lua"))()

-- Criação da UI
local UI = Lib:Create{
    Theme = "Dark", -- Tema da interface
    Size = UDim2.new(0, 555, 0, 400) -- Tamanho da interface
}

local Main = UI:Tab{
    Name = "Inicia"
}

local Divider = Main:Divider{
    Name = "Funções"
}

local QuitDivider = Main:Divider{
    Name = "Sair"
}

-- Função para pegar todos os itens no mapa e colocar no inventário do jogador
local function giveAllItemsToPlayer(player)
    -- Verifica se o jogador tem um Backpack
    local backpack = player:WaitForChild("Backpack")

    -- Varre o Workspace para pegar todos os itens (Modelos, Ferramentas, etc.)
    for _, item in pairs(game.Workspace:GetChildren()) do
        -- Verifica se o item é uma ferramenta ou um modelo
        if item:IsA("Tool") or item:IsA("Model") then
            -- Cria uma cópia do item para evitar alterar o original no mapa
            local itemClone = item:Clone()

            -- Coloca a cópia do item no Backpack do jogador
            itemClone.Parent = backpack
        end
    end

    -- Mensagem para informar que os itens foram adicionados ao inventário
    print("Todos os itens foram colocados no inventário do jogador!")
end

-- Botão para dar todos os itens ao jogador
local GiveItemsButton = Divider:Button{
    Name = "Pegar todos os itens e colocar no inventário",
    Callback = function()
        -- Pegando o jogador local (isso funciona se for para o jogador local)
        local player = game.Players.LocalPlayer
        giveAllItemsToPlayer(player)
    end
}

-- Botão para fechar a UI
local Quit = QuitDivider:Button{
    Name = "Fechar a biblioteca UI.",
    Callback = function()
        UI:Quit{
            Message = "Saindo...", -- Mensagem ao fechar a interface
            Length = 1 -- Tempo em segundos que a mensagem fica visível
        }
    end
}
