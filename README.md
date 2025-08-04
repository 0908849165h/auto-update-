--[[
  🔰 GG SCRIPT PRO UI v1 🔰
  📅 2025-08-04
  ✨ Auto Update từ Github
]]

local file ="/storage/emulated/0/pass.txt"
local correct_pass = "123456" -- thay mật khẩu tại đây

-- Hàm kiểm tra file tồn tại
local function fileExists(path)
  local f = io.open(path, "r")
  if f then f:close() return true else return false end
end

-- Hàm ghi mật khẩu mới
local function writePassword(pass)
  local f = io.open(file, "w")
  f:write(pass)
  f:close()
end

-- Hàm đọc mật khẩu đã lưu
local function readPassword()
  local f = io.open(file, "r")
  local data = f:read("*a")
  f:close()
  return data
end

-- Nếu chưa có file, yêu cầu nhập và lưu mật khẩu
if not fileExists(file) then
  local input = gg.prompt({"Nhập mật khẩu:"}, {""})[1]
  if not input or input == "" then
    gg.alert("Không nhập mật khẩu. Thoát.")
    os.exit()
  end
  writePassword(input)
end

-- Đọc mật khẩu từ file và kiểm tra
local saved_pass = readPassword()
if saved_pass ~= correct_pass then
  gg.alert("Sai mật khẩu! Script dừng lại.")
  os.exit()
end

gg.alert("✅ Đăng nhập thành công!")

local CURRENT_VERSION = "1 beta"
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
║ 🔰 GG Script Pro UI v1  ║
║ 👤 Tác giả: @Hieudzzzzcuto  ║
║ 🔄 Auto Update từ Github║
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
end    if not resp or resp.code ~= 200 then
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
