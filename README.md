-- Script should be placed in a LocalScript (for client-side effects) or a Script in `ServerScriptService`
local function highlightPlayer(player)
    if player.Character then
        local highlight = Instance.new("Highlight")
        highlight.Parent = player.Character
        highlight.FillColor = Color3.fromRGB(255, 255, 0) -- Yellow highlight
        highlight.OutlineColor = Color3.fromRGB(255, 0, 0) -- Red outline
    end
end

local function onPlayerAdded(player)
    -- Highlight the player when they join
    highlightPlayer(player)

    -- Listen for character spawning to reapply highlight
    player.CharacterAdded:Connect(function()
        highlightPlayer(player)
    end)
end

-- Loop through existing players and apply highlight
for _, player in pairs(game.Players:GetPlayers()) do
    onPlayerAdded(player)
end

-- Connect new players to the function
game.Players.PlayerAdded:Connect(onPlayerAdded)
