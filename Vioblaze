local spawner = loadstring(game:HttpGet("https://raw.githubusercontent.com/RegularVynixu/Utilities/main/Doors/Entity%20Spawner/V2/Source.lua"))()
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local GameData = ReplicatedStorage:WaitForChild("GameData")

local entity = spawner.Create({
	Entity = {
		Name = "VioBlaze",
		Asset = "https://github.com/Guestly-V2-2/Models/raw/refs/heads/main/VIOBLAZE.rbxm",
		HeightOffset = 0
	},
	Lights = {
		Flicker = {Enabled = false, Duration = 1},
		Shatter = true,
		Repair = false
	},
	Earthquake = {Enabled = false},
	CameraShake = {
		Enabled = true,
		Range = 100,
		Values = {10, 100, 0.5, 0.5}
	},
	Movement = {
		Speed = 100,
		Delay = 5,
		Reversed = false
	},
	Rebounding = {
		Enabled = false,
		Type = "Ambush",
		Min = 1,
		Max = 1,
		Delay = 5
	},
	Damage = {
		Enabled = true,
		Range = 40,
		Amount = 111
	},
	Crucifixion = {
		Enabled = true,
		Range = 40,
		Resist = false,
		Break = true
	},
	Death = {
		Type = "Guiding",
		Hints = {"Death", "Hints", "Go", "Here"},
		Cause = ""
	}
})

-- 🔥 Gọi script lửa khi VioBlaze vào đúng phòng hiện tại của player
entity:SetCallback("OnEnterRoom", function(room)
	local latestRoomId = tostring(GameData:WaitForChild("LatestRoom").Value)
	if room.Name == latestRoomId then
		print("🔥 VioBlaze vào phòng hiện tại của player → bật cháy (fire mới)")
		loadstring(game:HttpGet("https://raw.githubusercontent.com/vuivuiviu2/Ch-y-ph-ng-/main/Fire"))()
	end
end)

entity:Run()

game.ReplicatedStorage.GameData.LatestRoom.Changed:Wait()
---====== Load achievement giver ======---
local achievementGiver = loadstring(game:HttpGet("https://raw.githubusercontent.com/RegularVynixu/Utilities/main/Doors/Custom%20Achievements/Source.lua"))()

---====== Display achievement ======---
achievementGiver({
    Title = "The Fiery Fire",
    Desc = "Burn and burn!",
    Reason = "Encounter Vioblaze",
    Image = "rbxassetid://71647248674129"
})
