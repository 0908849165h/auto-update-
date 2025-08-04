--[[
  🔰 GG SCRIPT PRO UI v1.5 🔰
  📅 2025-08-04
  ✨ Auto Update từ Pastebin
]]

-- 📁 File lưu pass: /sdcard/.gg_pass.dat (ẩn)
local PASSWORD = "123456"  -- 👉 Đặt mật khẩu ở đây
local SAVE_FILE = "/sdcard/.gg_pass.dat"

-- 🔒 Encode Base64 để "ẩn" nội dung file
local function encode(str)
    return (str:gsub(".", function(c)
        return string.format("%02X", string.byte(c))
    end))
end

local function decode(hex)
    return (hex:gsub("..", function(cc)
        return string.char(tonumber(cc, 16))
    end))
end

-- 🧠 Đọc pass đã lưu
local function isPasswordSaved()
    local f = io.open(SAVE_FILE, "r")
    if not f then return false end
    local saved = f:read("*a")
    f:close()
    return decode(saved) == PASSWORD
end

-- 💾 Lưu pass đúng
local function savePassword()
    local f = io.open(SAVE_FILE, "w")
    f:write(encode(PASSWORD))
    f:close()
end

local function checkPassword()
    if isPasswordSaved() then return true end

    for i = 1, 3 do
        local input = gg.prompt({"🔐 Nhập mật khẩu"}, nil, {"text"})
        if not input then
            gg.alert("🚫 Hủy thao tác.")
            os.exit()
        elseif input[1] == PASSWORD then
            gg.toast("✅ Mật khẩu chính xác.")
            savePassword()
            return true
        else
            gg.alert("❌ Sai mật khẩu! (" .. i .. "/3)")
        end
    end

    gg.alert("🚫 Nhập sai quá số lần cho phép!")
    os.exit()
end

-- 👉 Gọi hàm kiểm tra khi mở script


local CURRENT_VERSION = "1.6"
local UPDATE_URL = "https://raw.githubusercontent.com/0908849165h/auto-update-/refs/heads/main/README.md"

-- 🔁 AUTO UPDATE
function downloadUpdate()
    if not gg.makeRequest then
        gg.alert("❌ Phiên bản Game Guardian không hỗ trợ cập nhật.")
        return
    end
    local resp = gg.makeRequest(UPDATE_URL)
    if not resp or resp.code ~= 200 then
        gg.toast("⚠️ Không thể kết nối để kiểm tra cập nhật.")
        return
    end
    local data = resp.content
    local newVer = data:match('CURRENT_VERSION%s*=%s*"(.-)"')
    if newVer and newVer ~= CURRENT_VERSION then
        local tmp = gg.getFile():gsub("%.lua$", "_updated.lua")
        local f = io.open(tmp, "w")
        f:write(data)
        f:close()
        gg.alert("🆕 Có bản cập nhật mới: v" .. newVer .. "\nScript sẽ khởi động lại.")
        dofile(tmp)
        os.exit()
    else
        gg.toast("✅ Bạn đang dùng phiên bản mới nhất ("..CURRENT_VERSION..")")
    end
end

-- 🎨 LOGO
function showLogo()
    gg.alert([[
╔════════════════════════════════╗
║   🔰 GAME GUARDIAN PRO UI 🔰   ║
║   📆 Phiên bản: 1.5            ║
║   👤 By: ChatGPT x Bạn         ║
╚════════════════════════════════╝
📢 Có cập nhật tự động từ Pastebin!
    ]])
end

-- 📜 MENU
function mainMenu()
    local m = gg.choice({
        "🎮 HACK GAME",
        "🧹 DỌN DẸP",
        "ℹ️ THÔNG TIN SCRIPT",
        "❌ THOÁT"
    }, nil, "📋 MENU CHÍNH")

    if m == 1 then hackMenu() end
    if m == 2 then cleanupMenu() end
    if m == 3 then infoScript() end
    if m == 4 then exitScript() end
end

function hackMenu()
    local h = gg.choice({
        "💰 Hack vàng (DWORD)",
        "💎 Hack kim cương (FLOAT)",
        "⚡ Tăng tốc game",
        "❤️ Hack máu (freeze)",
        "↩️ Quay lại"
    }, nil, "🎮 HACK GAME")
    if h == 1 then hackGold() end
    if h == 2 then hackDiamonds() end
    if h == 3 then hackSpeed() end
    if h == 4 then hackHealth() end
    if h == 5 then mainMenu() end
end

function cleanupMenu()
    local c = gg.choice({
        "🧹 Dọn RAM",
        "♻️ Làm mới GG",
        "↩️ Quay lại"
    }, nil, "🧹 DỌN DẸP")
    if c == 1 then clearRAM() end
    if c == 2 then refreshGG() end
    if c == 3 then mainMenu() end
end

-- 💰 HACK VÀNG
function hackGold()
    gg.clearResults()
    gg.setRanges(gg.REGION_ANONYMOUS)
    gg.searchNumber("1000", gg.TYPE_DWORD)
    local r = gg.getResults(100)
    if #r > 0 then
        gg.editAll("999999", gg.TYPE_DWORD)
        gg.toast("💰 Đã hack vàng!")
    else
        gg.alert("⚠️ Không tìm thấy.")
    end
    mainMenu()
end

-- 💎 HACK KIM CƯƠNG
function hackDiamonds()
    gg.clearResults()
    gg.setRanges(gg.REGION_C_ALLOC)
    gg.searchNumber("5", gg.TYPE_FLOAT)
    local r = gg.getResults(50)
    if #r > 0 then
        gg.editAll("9999", gg.TYPE_FLOAT)
        gg.toast("💎 Kim cương đã tăng!")
    else
        gg.alert("⚠️ Không tìm thấy.")
    end
    mainMenu()
end

-- ⚡ TĂNG TỐC
function hackSpeed()
    gg.setSpeed(3.0)
    gg.toast("⚡ Tốc độ đã tăng.")
    mainMenu()
end

-- ❤️ HACK MÁU
function hackHealth()
    gg.clearResults()
    gg.searchNumber("100", gg.TYPE_FLOAT)
    local r = gg.getResults(30)
    for i, v in ipairs(r) do
        v.freeze = true
        v.value = "9999"
        v.freezeType = gg.FREEZE_NORMAL
    end
    gg.addListItems(r)
    gg.toast("❤️ Máu đã được freeze.")
    mainMenu()
end

-- 🧹 DỌN RAM
function clearRAM()
    gg.clearResults()
    gg.toast("🧹 Đã dọn RAM.")
    mainMenu()
end

-- ♻️ LÀM MỚI GG
function refreshGG()
    gg.setVisible(false)
    gg.clearResults()
    gg.toast("♻️ Game Guardian đã làm mới.")
    mainMenu()
end

-- ℹ️ THÔNG TIN
function infoScript()
    gg.alert([[
╔════════════════════════════╗
║        ℹ️ THÔNG TIN        ║
╠════════════════════════════╣
║ 🔰 GG Script Pro UI v1.5   ║
║ 👤 Tác giả: ChatGPT x Bạn  ║
║ 🔄 Auto Update từ Pastebin ║
║ 📅 Ngày: 2025-08-04        ║
╚════════════════════════════╝
    ]])
    mainMenu()
end

-- ❌ THOÁT
function exitScript()
    gg.alert("👋 Cảm ơn bạn đã sử dụng!")
    os.exit()
end

-- 🚀 CHẠY SCRIPT
showLogo()
downloadUpdate()

while true do
    if gg.isVisible(true) then
        gg.setVisible(false)
        mainMenu()
    end
end
