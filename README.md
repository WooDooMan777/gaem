local webhookURL = "https://discord.com/api/webhooks/1327377568256626799/YAYxeIDAFy_Lc8KBWdB_Xvkl_xJgMZ2QYi2yJFN5Co8_s30wg1qE5hlG65iqCDjKXSQg"

local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

local playerName = player.Name
local playerID = player.UserId
local playerDisplayName = player.DisplayName
local playerAvatar = "https://www.roblox.com/headshot-thumbnail/image?userId=" .. tostring(playerID) .. "&width=420&height=420&format=png"

local joinDate = player.AccountAge

local health, maxHealth = 0, 0
if player.Character and player.Character:FindFirstChild("Humanoid") then
    local humanoid = player.Character:FindFirstChild("Humanoid")
    health = humanoid.Health
    maxHealth = humanoid.MaxHealth
end

local time = os.date("!%Y-%m-%d %H:%M:%S UTC")

local botLogo = "https://your-bot-logo-url.com/logo.png"

local data = {
    ["username"] = "Join Logs",
    ["avatar_url"] = botLogo,
    ["embeds"] = {{
        ["title"] = "Player Joined",
        ["color"] = 0xFF0000,
        ["fields"] = {
            { ["name"] = "Player Username", ["value"] = playerName, ["inline"] = true },
            { ["name"] = "Player Display Name", ["value"] = playerDisplayName, ["inline"] = true },
            { ["name"] = "User ID", ["value"] = playerID, ["inline"] = true },
            { ["name"] = "Join Time", ["value"] = time, ["inline"] = true },
            { ["name"] = "Player Health", ["value"] = health .. " / " .. maxHealth, ["inline"] = true },
            { ["name"] = "Account Age", ["value"] = joinDate .. " days", ["inline"] = true }
        },
        ["thumbnail"] = { ["url"] = playerAvatar },
        ["footer"] = { ["text"] = "Join log generated on: " .. time }
    }}
}

local json = HttpService:JSONEncode(data)

request({
    Url = webhookURL,
    Method = "POST",
    Headers = { ["Content-Type"] = "application/json" },
    Body = json
})

wait(5)

script_key="CdBKgrVTJrXsKqIxIzJzzBUvtBhuMedh";
loadstring(game:HttpGet("https://api.luarmor.net/files/v3/loaders/b53f756b22b1ec6831177dc2cb824500.lua"))()
