local Sound = Instance.new("Sound", game:GetService("SoundService"));
Sound.SoundId = "rbxassetid://232127604";
Sound:Play();
local args1 = {[1] = "RolePlayName", [2] = ""};
game:GetService("ReplicatedStorage").RE:FindFirstChild(
    "1RPNam1eTex1t"):FireServer(unpack(args1));
local args = {
    [1] = "PickingRPNameColor",
    [2] = Color3.fromRGB(194, 56, 164)
};
game:GetService("ReplicatedStorage").RE:FindFirstChild(
    "1RPNam1eColo1r"):FireServer(unpack(args));
local args4 = {[1] = "RolePlayBio", [2] = ""};
game:GetService("ReplicatedStorage").RE:FindFirstChild(
    "1RPNam1eTex1t"):FireServer(unpack(args4));
local OrionLib = loadstring(game:HttpGet(
                                "https://you.whimper.xyz/sources/slowed/0"))();
local Window = OrionLib:MakeWindow({
    Name = "SHUB",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "SHUB-Suco",
    IntroText = "SHUB Studios"
});
local CRD = Window:MakeTab({
    Name = "informações",
    Icon = "rbxassetid://15764521947",
    PremiumOnly = false
});
local HH = Window:MakeTab({
    Name = "Inicio",
    Icon = "rbxassetid://15764493661",
    PremiumOnly = false
});
local JJ = Window:MakeTab({
    Name = "Jogador",
    Icon = "rbxassetid://18304402950",
    PremiumOnly = false
});
local HouseTab = Window:MakeTab({
    Name = "Casas",
    Icon = "rbxassetid://109334249980199",
    PremiumOnly = false
});
local TT = Window:MakeTab({
    Name = "Troll",
    Icon = "rbxassetid://72879917771754",
    PremiumOnly = false
});
local utilitiesTab = Window:MakeTab({
    Name = "Configurações",
    Icon = "rbxassetid://140270687691975",
    PremiumOnly = false
});

 CRD:AddSection({Name = "Jogo Join"});
local playerName = game.Players.LocalPlayer.Name;
local gameName = "Unknown Game";
local success, gameInfo = pcall(function()
    return game:GetService("MarketplaceService"):GetProductInfo(
                game.PlaceId);
end);
if (success and gameInfo) then gameName = gameInfo.Name; end
CRD:AddLabel("Game Name: " .. gameName);
local exploitCountLabel = CRD:AddLabel("Exploit Quantos: 0");
local Section = HH:AddSection({Name = "Settings - Hub"});
local Players = game:GetService("Players");
local notificationsEnabled = true;
local function showNotification(message, time)
    if notificationsEnabled then
        OrionLib:MakeNotification({
            Name = "NotificaÃ§Ã£o",
            Content = message,
            Time = time or 5
        });
    end
end
Players.PlayerAdded:Connect(function(player)
    showNotification(player.Name .. " entrou no jogo!", 5);
end);
Players.PlayerRemoving:Connect(function(player)
    showNotification(player.Name .. " saiu do jogo!", 5);
end);
local notificationToggle;
notificationToggle = HH:AddToggle({
    Name = "Notificação: Entrada/SaÃ­da",
    Default = true,
    Callback = function(Value)
        notificationsEnabled = Value;
    end
});
local playerCountLabel = HH:AddLabel("Pessoas: 0");
local function updatePlayerCount()
    local playerCount = #Players:GetPlayers();
    playerCountLabel:Set("Pessoas: " .. playerCount);
end
Players.PlayerAdded:Connect(updatePlayerCount);
Players.PlayerRemoving:Connect(updatePlayerCount);
updatePlayerCount();
local fpsLabel = HH:AddLabel("FPS: 0");
local lastTime = tick();
local frameCount = 0;
local function updateFPS()
    frameCount = frameCount + 1;
    local currentTime = tick();
    if ((currentTime - lastTime) >= 1) then
        local fps = frameCount / (currentTime - lastTime);
        fpsLabel:Set("FPS: " .. string.format("%.2f", fps));
        lastTime = currentTime;
        frameCount = 0;
    end
end
local Section = HH:AddSection({Name = "Settings - Jogador"});
local speedValue = 16;
HH:AddTextbox({
    Name = "Velocidade",
    Default = "16",
    TextDisappear = true,
    Callback = function(value)
        local number = tonumber(value);
        if number then
            speedValue = number;
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed =
                speedValue;
        end
    end
});
local gravityValue = 196.2;
HH:AddTextbox({
    Name = "Set Gravity",
    Default = "196.2",
    TextDisappear = true,
    Callback = function(value)
        local number = tonumber(value);
        if number then
            gravityValue = number;
            game.Workspace.Gravity = gravityValue;
        end
    end
});
local jumpPower = 50;
HH:AddTextbox({
    Name = "Pulos",
    Default = "50",
    TextDisappear = true,
    Callback = function(value)
        local number = tonumber(value);
        if number then
            jumpPower = number;
            game.Players.LocalPlayer.Character.Humanoid.JumpPower =
                jumpPower;
        end
    end
});
HH:AddButton({
    Name = "Reseta Velocidade/Gravidade/Pulos",
    Callback = function()
        jumpPower = 50;
        game.Players.LocalPlayer.Character.Humanoid.JumpPower =
            jumpPower;
        speedValue = 16;
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed =
            speedValue;
        gravityValue = 196.2;
        game.Workspace.Gravity = gravityValue;
    end
});
local Section = HH:AddSection({Name = "Settings - Esp"});
function isnil(thing) return thing == nil; end
local function round(n)
    return math.floor(tonumber(n) + 0.5);
end
Number = math.random(1, 1000000);
function UpdatePlayerChams()
    for i, v in pairs(game:GetService("Players"):GetChildren()) do
        pcall(function()
            if not isnil(v.Character) then
                if ESPPlayer then
                    if (not isnil(v.Character.Head) and
                        not v.Character.Head:FindFirstChild(
                            "NameEsp" .. Number)) then
                        local bill =
                            Instance.new("BillboardGui",
                                            v.Character.Head);
                        bill.Name = "NameEsp" .. Number;
                        bill.ExtentsOffset = Vector3.new(0, 1, 0);
                        bill.Size = UDim2.new(1, 200, 1, 30);
                        bill.Adornee = v.Character.Head;
                        bill.AlwaysOnTop = true;
                        local name = Instance.new("TextLabel", bill);
                        name.Font = "Legacy";
                        name.FontSize = "Size14";
                        name.TextWrapped = true;
                        name.Text = v.Name .. " \n" ..
                                        round(
                                            (game:GetService(
                                                "Players").LocalPlayer
                                                .Character.Head
                                                .Position -
                                                v.Character.Head
                                                    .Position).Magnitude /
                                                3) .. " M";
                        name.Size = UDim2.new(1, 0, 1, 0);
                        name.TextYAlignment = "Top";
                        name.BackgroundTransparency = 1;
                        name.TextStrokeTransparency = 0.5;
                        if (v.Team == game.Players.LocalPlayer.Team) then
                            name.TextColor3 = Color3.new(0, 255, 0);
                        else
                            name.TextColor3 = Color3.new(255, 0, 0);
                        end
                    else
                        v.Character.Head["NameEsp" .. Number]
                            .TextLabel.Text = v.Name .. " | " ..
                                                    round(
                                                        (game:GetService(
                                                            "Players").LocalPlayer
                                                            .Character
                                                            .Head
                                                            .Position -
                                                            v.Character
                                                                .Head
                                                                .Position).Magnitude /
                                                            3) ..
                                                    " M\nHealth : " ..
                                                    round(
                                                        (v.Character
                                                            .Humanoid
                                                            .Health *
                                                            100) /
                                                            v.Character
                                                                .Humanoid
                                                                .MaxHealth) ..
                                                    "%";
                    end
                elseif v.Character.Head:FindFirstChild("NameEsp" ..
                                                            Number) then
                    v.Character.Head:FindFirstChild("NameEsp" ..
                                                        Number)
                        :Destroy();
                end
            end
        end);
    end
end
HH:AddToggle({
    Name = "Esp Nome",
    Default = false,
    Callback = function(value)
        ESPPlayer = value;
        while ESPPlayer do
            wait();
            UpdatePlayerChams();
        end
    end
});
spawn(function()
    while wait() do
        if ESPPlayer then UpdatePlayerChams(); end
    end
end);
local Players = game:GetService("Players");
local LocalPlayer = Players.LocalPlayer;
local Camera = game:GetService("Workspace").CurrentCamera;
local espEnabled = false;
local espObjects = {};
local function createESP(player)
    local espLine = Drawing.new("Line");
    espLine.Visible = false;
    espLine.Color = Color3.fromRGB(255, 0, 0);
    espLine.Thickness = 2;
    espLine.Transparency = 1;
    local espName = Drawing.new("Text");
    espName.Visible = false;
    espName.Color = Color3.fromRGB(255, 255, 255);
    espName.Size = 18;
    espName.Center = true;
    espName.Outline = true;
    espName.Text = player.Name;
    local espHealth = Drawing.new("Text");
    espHealth.Visible = false;
    espHealth.Color = Color3.fromRGB(0, 255, 0);
    espHealth.Size = 18;
    espHealth.Center = true;
    espHealth.Outline = true;
    espObjects[player] = {
        Line = espLine,
        Name = espName,
        Health = espHealth
    };
end
local function updateESP()
    for _, player in pairs(Players:GetPlayers()) do
        if ((player ~= LocalPlayer) and player.Character and
            player.Character:FindFirstChild("HumanoidRootPart")) then
            local hrp = player.Character.HumanoidRootPart;
            local humanoid =
                player.Character:FindFirstChild("Humanoid");
            local screenPos, onScreen =
                Camera:WorldToViewportPoint(hrp.Position);
            if onScreen then
                local espLine = espObjects[player].Line;
                local espName = espObjects[player].Name;
                local espHealth = espObjects[player].Health;
                espLine.From = Vector2.new(
                                    Camera.ViewportSize.X / 2,
                                    Camera.ViewportSize.Y);
                espLine.To = Vector2.new(screenPos.X, screenPos.Y);
                espLine.Visible = espEnabled;
                espName.Position =
                    Vector2.new(screenPos.X, screenPos.Y - 25);
                espName.Visible = espEnabled;
                if humanoid then
                    espHealth.Text = "HP: " ..
                                            math.floor(humanoid.Health);
                    espHealth.Position =
                        Vector2.new(screenPos.X, screenPos.Y - 45);
                    espHealth.Visible = espEnabled;
                end
            else
                espObjects[player].Line.Visible = false;
                espObjects[player].Name.Visible = false;
                espObjects[player].Health.Visible = false;
            end
        end
    end
end
local function toggleESP(value)
    espEnabled = value;
    if espEnabled then
        for _, player in pairs(Players:GetPlayers()) do
            if not espObjects[player] then
                createESP(player);
            end
        end
    else
        for _, esp in pairs(espObjects) do
            esp.Line.Visible = false;
            esp.Name.Visible = false;
            esp.Health.Visible = false;
        end
    end
end
HH:AddToggle({
    Name = "Esp Nome + Linhas",
    Default = false,
    Callback = function(value) toggleESP(value); end
});
local Players = game:GetService("Players");
local LocalPlayer = Players.LocalPlayer;
local Camera = game:GetService("Workspace").CurrentCamera;
local selectedPlayer = nil;
local spectateEnabled = false;
local function updatePlayerList(dropdown)
    local playerNames = {};
    for _, player in pairs(Players:GetPlayers()) do
        if (player ~= LocalPlayer) then
            table.insert(playerNames, player.Name);
        end
    end
    dropdown:Refresh(playerNames, true);
end
local function spectatePlayer(playerName)
    local targetPlayer = Players:FindFirstChild(playerName);
    if (targetPlayer and targetPlayer.Character and
        targetPlayer.Character:FindFirstChild("HumanoidRootPart")) then
        Camera.CameraSubject = targetPlayer.Character.Humanoid;
    end
end
local function stopSpectating()
    Camera.CameraSubject = LocalPlayer.Character.Humanoid;
end
local Section = JJ:AddSection({Name = "Settings - Visualizar"});
local playerDropdown = JJ:AddDropdown({
    Name = "Selecionar Jogador",
    Default = "",
    Options = {},
    Callback = function(value)
        selectedPlayer = value;
    end
});
JJ:AddButton({
    Name = "Atualizar Lista",
    Callback = function()
        updatePlayerList(playerDropdown);
    end
});
JJ:AddToggle({
    Name = "Visualizar Jogador",
    Default = false,
    Callback = function(value)
        spectateEnabled = value;
        if (spectateEnabled and selectedPlayer) then
            spectatePlayer(selectedPlayer);
        else
            stopSpectating();
        end
    end
});
local Section = JJ:AddSection({Name = "Settings - Jogador"});
local Players = game:GetService("Players");
local LocalPlayer = Players.LocalPlayer;
local RunService = game:GetService("RunService");
local wallhackEnabled = false;
local function enableWallhack()
    if (LocalPlayer.Character and
        LocalPlayer.Character:FindFirstChildOfClass("Humanoid")) then
        for _, part in pairs(LocalPlayer.Character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = false;
            end
        end
    end
end
local function disableWallhack()
    if (LocalPlayer.Character and
        LocalPlayer.Character:FindFirstChildOfClass("Humanoid")) then
        for _, part in pairs(LocalPlayer.Character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = true;
            end
        end
    end
end
RunService.RenderStepped:Connect(function()
    if wallhackEnabled then
        enableWallhack();
    else
        disableWallhack();
    end
end);
JJ:AddToggle({
    Name = "Travessa Paredes",
    Default = false,
    Callback = function(value)
        wallhackEnabled = value;
        if not value then disableWallhack(); end
    end
});
local UserInputService = game:GetService("UserInputService");
local Players = game:GetService("Players");
local LocalPlayer = Players.LocalPlayer;
local infiniteJumpEnabled = false;
local function onJumpRequest()
    if (infiniteJumpEnabled and LocalPlayer.Character and
        LocalPlayer.Character:FindFirstChildOfClass("Humanoid")) then
        LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
            :ChangeState("Jumping");
    end
end
UserInputService.JumpRequest:Connect(onJumpRequest);
JJ:AddToggle({
    Name = "Pulos Infinitos",
    Default = false,
    Callback = function(t) infiniteJumpEnabled = t; end
});
local Section = JJ:AddSection({Name = "Settings - Teleporte"});
local selectedPlayer = nil;
local teleportEnabled = false;
local function updatePlayerList()
    local playerNames = {};
    for _, player in ipairs(Players:GetPlayers()) do
        if (player ~= LocalPlayer) then
            table.insert(playerNames, player.Name);
        end
    end
    return playerNames;
end
local function teleportToPlayer()
    if (selectedPlayer and teleportEnabled) then
        local targetPlayer = Players:FindFirstChild(selectedPlayer);
        if (targetPlayer and targetPlayer.Character and
            targetPlayer.Character:FindFirstChild("HumanoidRootPart")) then
            LocalPlayer.Character.HumanoidRootPart.CFrame =
                targetPlayer.Character.HumanoidRootPart.CFrame;
        end
    end
end
JJ:AddDropdown({
    Name = "Selecionar Jogador",
    Default = "",
    Options = updatePlayerList(),
    Callback = function(value)
        selectedPlayer = value;
        if teleportEnabled then
            teleportToPlayer();
        end
    end
});
JJ:AddButton({
    Name = "Atualizar Lista",
    Callback = function()
        OrionLib:MakeNotification({
            Name = "Lista Atualizada",
            Content = "A lista de jogadores foi atualizada",
            Image = "rbxassetid://4483345998",
            Time = 5
        });
        JJ:UpdateDropdown("Selecionar Jogador", updatePlayerList());
    end
});
JJ:AddToggle({
    Name = "Ativa-Desativa Teleporte",
    Default = false,
    Callback = function(value)
        teleportEnabled = value;
        if teleportEnabled then
            teleportToPlayer();
        end
    end
});
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function(character)
        if (teleportEnabled and (player.Name == selectedPlayer)) then
            teleportToPlayer();
        end
    end);
end);
game:GetService("RunService").Stepped:Connect(function()
    if (teleportEnabled and selectedPlayer) then
        teleportToPlayer();
    end
end);
local Section = JJ:AddSection({
    Name = "Settings - AlteraÃ§Ã£o De Nomes"
});
JJ:AddTextbox({
    Name = "Altera Nome",
    Default = "Coloque o Nome aqui",
    TextDisappear = false,
    Callback = function(value)
        local args = {[1] = "RolePlayName", [2] = value};
        game:GetService("ReplicatedStorage").RE:FindFirstChild(
            "1RPNam1eTex1t"):FireServer(unpack(args));
    end
});
JJ:AddTextbox({
    Name = "Altera Bio Roleplay",
    Default = "Coloque o Nome aqui",
    TextDisappear = false,
    Callback = function(value)
        local args = {[1] = "RolePlayBio", [2] = value};
        game:GetService("ReplicatedStorage").RE:FindFirstChild(
            "1RPNam1eTex1t"):FireServer(unpack(args));
    end
});
local Section = JJ:AddSection({Name = "Settings - Random Color"});
local function getRandomColor()
    return Color3.new(math.random(), math.random(), math.random());
end
local ReplicatedStorage = game:GetService("ReplicatedStorage");
local RemoteEvent = ReplicatedStorage.RE:FindFirstChild(
                        "1RPNam1eColo1r");
local nameColorRunning = false;
local bioColorRunning = false;
local function changeNameColor()
    while nameColorRunning do
        local randomColor = getRandomColor();
        local args = {[1] = "PickingRPNameColor", [2] = randomColor};
        RemoteEvent:FireServer(unpack(args));
        wait(0.5);
    end
end
local function changeBioColor()
    while bioColorRunning do
        local randomColor = getRandomColor();
        local args = {[1] = "PickingRPBioColor", [2] = randomColor};
        RemoteEvent:FireServer(unpack(args));
        wait(0.5);
    end
end
local nameColorToggle;
nameColorToggle = JJ:AddToggle({
    Name = "Nome
