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
-- Janela principal do script
local Window = OrionLib:MakeWindow({
    Name = "SHUB",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "Team SHUB",
    IntroText = "SHUB Studios"
});
-- Tabs
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

local AA = Window:MakeTab({
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

-- notificaçãoes 
local Section = CRD:AddSection({Name = "Jogo Join"});
local playerName = game.Players.LocalPlayer.Name;
local gameName = "Unknown Game";
local success, gameInfo = pcall(function()
    return game:GetService("MarketplaceService"):GetProductInfo(
                game.PlaceId);
end);
if (success and gameInfo) then gameName = gameInfo.Name; end
CRD:AddLabel("Game Name: " .. gameName);

local Players = game:GetService("Players");
local notificationsEnabled = true;
local function showNotification(message, time)
    if notificationsEnabled then
        OrionLib:MakeNotification({
            Name = "Notificação",
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

-- mexer no player
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
-- ih
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

-- casas
local houseNumbers = {
    1, 2, 3, 4, 5, 6, 7, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,
    22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37
};
local selectedHouseNumber = nil;
HouseTab:AddDropdown({
    Name = "Selecione a Casa",
    Options = houseNumbers,
    Default = 1,
    Callback = function(Value)
        selectedHouseNumber = tonumber(Value);
        print("Casa selecionada:", selectedHouseNumber);
    end
});

HouseTab:AddButton({
    Name = "Dar PermissÃ£o",
    Callback = function()
        if selectedHouseNumber then
            local args = {
                [1] = "GivePermissionLoopToServer",
                [2] = game:GetService("Players").LocalPlayer,
                [3] = selectedHouseNumber
            };
            game:GetService("ReplicatedStorage").RE:FindFirstChild(
                "1Playe1rTrigge1rEven1t"):FireServer(unpack(args));
            print("PermissÃ£o dada para a casa:",
                    selectedHouseNumber);
        else
            print("Nenhuma casa selecionada!");
        end
    end
});

HouseTab:AddButton({
    Name = "Remover Ban",
    Callback = function()
        if selectedHouseNumber then
            local lotNumber = "0o1.L0ts";
            local lot = workspace:FindFirstChild(lotNumber);
            if lot then
                for _, house in pairs(lot:GetChildren()) do
                    if house:FindFirstChild("HousePickedByPlayer") then
                        local bannedBlockName = "BannedBlock" ..
                                                    selectedHouseNumber;
                        local bannedBlock =
                            house.HousePickedByPlayer.HouseModel:FindFirstChild(
                                bannedBlockName);
                        if bannedBlock then
                            bannedBlock:Destroy();
                            print(bannedBlockName ..
                                        " deletado com sucesso em " ..
                                        house.Name);
                        else
                            print(bannedBlockName ..
                                        " nÃ£o encontrado em " ..
                                        house.Name);
                        end
                    end
                end
            else
                print("Lote " .. lotNumber .. " nÃ£o encontrado.");
            end
        else
            print("Nenhuma casa selecionada!");
        end
    end
});
local Section = TT:AddSection({Name = "Settings - Get"});
-- Troll
local Section = TT:AddSection({Name = "Settings - Get"});
TT:AddButton({
    Name = "Get guitarra (Sound)",
    Callback = function()
        loadstring(game:HttpGet(
                        "https://you.whimper.xyz/sources/slowed/1"))();
    end
});

TT:AddButton({
    Name = "Get Violao (Sound)",
    Callback = function()
        loadstring(game:HttpGet(
                        "https://you.whimper.xyz/sources/slowed/2"))();
    end
});

TT:AddButton({
    Name = "Get Sofa",
    Callback = function()
        loadstring(game:HttpGet("https://you.whimper.xyz/sources/slowed/3"))();
    end
});

TT:AddButton({
    Name = "Get Tp Tool",
    Callback = function()
        mouse = game.Players.LocalPlayer:GetMouse();
        tool = Instance.new("Tool");
        tool.RequiresHandle = false;
        tool.Name = "teleport";
        tool.Activated:connect(function()
            local pos = mouse.Hit + Vector3.new(0, 2.5, 0);
            pos = CFrame.new(pos.X, pos.Y, pos.Z);
            game.Players.LocalPlayer.Character.HumanoidRootPart
                .CFrame = pos;
        end);
        tool.Parent = game.Players.LocalPlayer.Backpack;
    end
});


local TweenService = game:GetService("TweenService");
local Players = game:GetService("Players");
local LocalPlayer = Players.LocalPlayer;
local Section = TT:AddSection({Name = "Settings - Orbitar"});
local selectedPlayer;
local orbiting = false;
local function getPlayers()
    local playerNames = {};
    for _, player in pairs(Players:GetPlayers()) do
        if (player ~= LocalPlayer) then
            table.insert(playerNames, player.Name);
        end
    end
    return playerNames;
end
local playerDropdown = TT:AddDropdown({
    Name = "Select Player",
    Default = "",
    Options = getPlayers(),
    Callback = function(value)
        selectedPlayer = Players:FindFirstChild(value);
    end
});



utilitiesTab:AddToggle({
    Name = "Anti Sit",
    Default = false,
    Callback = function(value)
        if value then
            RunService.Stepped:Connect(function()
                if (LocalPlayer.Character and
                    LocalPlayer.Character:FindFirstChild("Humanoid")) then
                    if LocalPlayer.Character.Humanoid.Sit then
                        LocalPlayer.Character.Humanoid.Sit = false;
                    end
                end
            end);
        end
    end
});

utilitiesTab:AddToggle({
    Name = "Anti Void",
    Default = false,
    Callback = function(value)
        if value then
            RunService.Stepped:Connect(function()
                if (LocalPlayer.Character and
                    LocalPlayer.Character:FindFirstChild(
                        "HumanoidRootPart")) then
                    if (LocalPlayer.Character.HumanoidRootPart
                        .Position.Y < -50) then
                        LocalPlayer.Character.HumanoidRootPart
                            .CFrame = CFrame.new(0, 50, 0);
                    end
                end
            end);
        end
    end
});

utilitiesTab:AddToggle({
    Name = "Auto Rejoin",
    Default = false,
    Callback = function(value)
        if value then
            game:GetService("CoreGui").RobloxPromptGui.promptOverlay
                .ChildAdded:Connect(function(child)
                if (child.Name == "ErrorPrompt") then
                    TeleportService:Teleport(game.PlaceId,
                                                LocalPlayer);
                end
            end);
        end
    end
});

utilitiesTab:AddToggle({
    Name = "Anti Lag",
    Default = false,
    Callback = function(value)
        if value then
            disableLaggyFeatures();
            workspace.DescendantAdded:Connect(
                function(descendant)
                    if (descendant:IsA("ParticleEmitter") or
                        descendant:IsA("Trail") or
                        descendant:IsA("Smoke") or
                        descendant:IsA("Fire")) then
                        descendant.Enabled = false;
                    end
                end);
        end
    end
});

local Section = utilitiesTab:AddSection({Name = "Settings"});
utilitiesTab:AddButton({
    Name = "Teleporta Pro Spaw",
    Callback = function()
        if (LocalPlayer.Character and
            LocalPlayer.Character:FindFirstChild("HumanoidRootPart")) then
            LocalPlayer.Character.HumanoidRootPart.CFrame =
                CFrame.new(0, 50, 0);
        end
    end
});

local function removeLag()
    for _, part in pairs(workspace:GetDescendants()) do
        if part:IsA("BasePart") then
            if not part.Visible then
                part:Destroy();
            elseif (part.Transparency >= 1) then
                part:Destroy();
            end
        end
    end
    for _, light in pairs(workspace:GetDescendants()) do
        if light:IsA("Light") then
            if (not light.Parent or not light.Parent.Parent) then
                light:Destroy();
            end
        end
    end
    for _, texture in pairs(workspace:GetDescendants()) do
        if texture:IsA("Texture") then
            if (texture.Parent and not texture.Parent.Visible) then
                texture:Destroy();
            end
        end
    end
    OrionLib:MakeNotification({
        Name = "Removendo...",
        Content = "Texturas, luzes e objetos invisiveis foram removidos.",
        Time = 5
    });
end

utilitiesTab:AddButton({
    Name = "Remover Lag",
    Callback = function() removeLag(); end
});
game:GetService("RunService").RenderStepped:Connect(updateESP);
updatePlayerList(playerDropdown);
RunService.RenderStepped:Connect(updateFPS);
OrionLib:Init();
print("Hi World :D");
local function detectExploits()
    local exploitCount = 0;
    for _, player in ipairs(Players:GetPlayers()) do
        if (player:FindFirstChild("HumanoidRootPart") and
            player.HumanoidRootPart.Anchored) then
            exploitCount = exploitCount + 1;
        end
    end
    return exploitCount;
end
local function updateExploitCount()
    local exploitCount = detectExploits();
    exploitCountLabel:Set("Exploit Quantos: " .. exploitCount);
end
Players.PlayerAdded:Connect(updateExploitCount);
Players.PlayerRemoving:Connect(updateExploitCount);
updateExploitCount();

local playerDropdown = TT:AddDropdown({
    Name = "Select Player",
    Default = "",
    Options = getPlayers(),
    Callback = function(value)
        selectedPlayer = Players:FindFirstChild(value);
    end
});

-- HH
AA:AddToggle({
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
-- Aqui
 AA:AddToggle({
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

local Section = AA:AddSection({Name = "Settings - Visualizar"});
local playerDropdown = JJ:AddDropdown({
    Name = "Selecionar Jogador",
    Default = "",
    Options = {},
    Callback = function(value)
        selectedPlayer = value;
    end
});

AA:AddButton({
    Name = "Atualizar Lista",
    Callback = function()
        updatePlayerList(playerDropdown);
    end
});

AA:AddToggle({
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

AA:AddToggle({
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
AA:AddToggle({
    Name = "Pulos Infinitos",
    Default = false,
    Callback = function(t) infiniteJumpEnabled = t; end
});


local Section = AA:AddSection({Name = "Settings - Teleporte"});
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

AA:AddDropdown({
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

AA:AddButton({
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

AA:AddToggle({
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
