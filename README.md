--[[
    Marketplace Shoulder Accessory
    Visible + Follow Arm Rotation
    GetObjects | Executor
    R6 & R15
--]]

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

-- 🔧 ID vật phẩm
local ASSET_ID = 4504231783

-- 🔧 Offset vị trí trên vai
local HEIGHT_OFFSET = 1.5
local SIDE_OFFSET   = 1.8
local FRONT_OFFSET  = 0

-- =========================
-- LOAD ASSET
-- =========================
local objects = game:GetObjects("rbxassetid://" .. ASSET_ID)
if not objects or #objects == 0 then
    warn("Không load được asset")
    return
end

-- =========================
-- FIND ACCESSORY
-- =========================
local acc0
for _, o in ipairs(objects) do
    if o:IsA("Accessory") then
        acc0 = o
        break
    elseif o:IsA("Model") then
        for _, v in ipairs(o:GetDescendants()) do
            if v:IsA("Accessory") then
                acc0 = v
                break
            end
        end
    end
end

if not acc0 then
    warn("Asset không phải Accessory")
    return
end

local acc = acc0:Clone()
acc.Parent = character

-- =========================
-- HANDLE
-- =========================
local handle = acc:FindFirstChild("Handle")
if not handle then
    warn("Accessory không có Handle")
    return
end

handle.Anchored = true       -- ⚠️ QUAN TRỌNG
handle.CanCollide = false
handle.Massless = true

-- =========================
-- R6 / R15 PARTS
-- =========================
local torso = character:FindFirstChild("UpperTorso") or character:FindFirstChild("Torso")
if not torso then
    warn("Không tìm thấy Torso")
    return
end

local arm =
    character:FindFirstChild("RightHand")
    or character:FindFirstChild("Right Arm")

if not arm then
    warn("Không tìm thấy tay phải")
    return
end

-- =========================
-- BASE OFFSET (VAI)
-- =========================
local baseOffset = CFrame.new(SIDE_OFFSET, HEIGHT_OFFSET, FRONT_OFFSET)

-- =========================
-- FOLLOW ARM ROTATION (HIỂN THỊ 100%)
-- =========================
RunService.RenderStepped:Connect(function()
    if not handle.Parent or not torso.Parent or not arm.Parent then return end

    -- lấy rotation tay
    local armRot = arm.CFrame - arm.CFrame.Position

    handle.CFrame =
        torso.CFrame
        * baseOffset
        * armRot
end)

print("✅ Accessory đã HIỆN và xoay theo tay player")
