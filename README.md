--[[
  🔰 GG SCRIPT PRO UI v1 🔰
  📅 2025-08-04
  ✨ Auto Update từ Github
]]

local file ="/storage/emulated/0/pass.txt"
local correct_pass = "ffob50nhucac" -- thay mật khẩu tại đây

-- Đa ngôn ngữ (Việt + English)
local lang = {}

lang["vi"] = {
    name = "Tiếng Việt",
    menuTitle = "📋 MENU CHÍNH",
    hackGame = "🎮 HACK GAME",
    cleanup = "🧹 DỌN DẸP",
    info = "ℹ️ THÔNG TIN SCRIPT",
    exit = "❌ THOÁT",
    chooseLang = "🌐 Chọn ngôn ngữ / Select language",
    countryOptions = {
        "🇻🇳 Việt Nam",
        "🇺🇸 English (US)",
        "🇧🇷 Brasil",
        "🇮🇩 Indonesia",
        "🇹🇭 Thái Lan",
        "🇮🇳 Ấn Độ",
        "🇷🇺 Nga",
        "🇲🇾 Malaysia",
        "🇲🇽 Mexico",
        "🇵🇭 Philippines",
        "↩️ Quay lại"
    },
    passPrompt = "Nhập mật khẩu:",
    passFail = "Sai mật khẩu! Script dừng lại.",
    passEmpty = "Không nhập mật khẩu. Thoát.",
    passSuccess = "✅ Đăng nhập thành công!",
    noUpdateSupport = "❌ Phiên bản Game Guardian không hỗ trợ cập nhật.",
    updateFail = "⚠️ Không thể kết nối để kiểm tra cập nhật.",
    updateNew = "🆕 Có bản cập nhật mới: v%s\nScript sẽ khởi động lại.",
    updateLatest = "✅ Bạn đang dùng phiên bản mới nhất (%s)",
    logo = [[
╔════════════════════════════════╗
║   🔰 GAME GUARDIAN PRO UI 🔰   ║
║   📆 Phiên bản: 1              ║
║   👤 By: @Hieudzzzzcuto        ║
╚════════════════════════════════╝
📢 Có cập nhật tự động từ Github!
]],
    menuHack = "🎮 HACK GAME",
    menuCleanup = "🧹 DỌN DẸP",
    menuInfo = "ℹ️ THÔNG TIN SCRIPT",
    menuExit = "❌ THOÁT",
    hackGold = "💰 Hack vàng (DWORD)",
    hackDiamonds = "💎 Hack kim cương (FLOAT)",
    hackSpeed = "⚡ Tăng tốc game",
    hackHealth = "❤️ Hack máu (freeze)",
    back = "↩️ Quay lại",
    hackGoldSuccess = "💰 Đã hack vàng!",
    hackGoldFail = "⚠️ Không tìm thấy.",
    hackDiamondSuccess = "💎 Kim cương đã tăng!",
    hackDiamondFail = "⚠️ Không tìm thấy.",
    hackSpeedSuccess = "⚡ Tốc độ đã tăng.",
    hackHealthSuccess = "❤️ Máu đã được freeze.",
    clearRAMSuccess = "🧹 Đã dọn RAM.",
    refreshGGSuccess = "♻️ Game Guardian đã làm mới.",
    infoText = [[
╔════════════════════════════╗
║        ℹ️ THÔNG TIN        ║
╠════════════════════════════╣
║ 🔰 GG Script Pro UI v1     ║
║ 👤 Tác giả: @Hieudzzzzcuto ║
║ 🔄 Auto Update từ Github   ║
║ 📅 Ngày: 2025-08-04       ║
╚════════════════════════════╝
]],
    goodbye = "👋 Cảm ơn bạn đã sử dụng!"
}

lang["en"] = {
    name = "English",
    menuTitle = "📋 MAIN MENU",
    hackGame = "🎮 HACK GAME",
    cleanup = "🧹 CLEANUP",
    info = "ℹ️ SCRIPT INFO",
    exit = "❌ EXIT",
    chooseLang = "🌐 Choose your language",
    countryOptions = {
        "🇻🇳 Vietnam",
        "🇺🇸 United States",
        "🇧🇷 Brazil",
        "🇮🇩 Indonesia",
        "🇹🇭 Thailand",
        "🇮🇳 India",
        "🇷🇺 Russia",
        "🇲🇾 Malaysia",
        "🇲🇽 Mexico",
        "🇵🇭 Philippines",
        "↩️ Back"
    },
    passPrompt = "Enter password:",
    passFail = "Wrong password! Script stopped.",
    passEmpty = "No password entered. Exiting.",
    passSuccess = "✅ Login successful!",
    noUpdateSupport = "❌ Game Guardian version does not support update.",
    updateFail = "⚠️ Cannot connect to check update.",
    updateNew = "🆕 New update found: v%s\nScript will restart.",
    updateLatest = "✅ You are using the latest version (%s)",
    logo = [[
╔════════════════════════════════╗
║   🔰 GAME GUARDIAN PRO UI 🔰   ║
║   📆 Version: 1                ║
║   👤 By: @Hieudzzzzcuto        ║
╚════════════════════════════════╝
📢 Auto update from Github!
]],
    menuHack = "🎮 HACK GAME",
    menuCleanup = "🧹 CLEANUP",
    menuInfo = "ℹ️ SCRIPT INFO",
    menuExit = "❌ EXIT",
    hackGold = "💰 Hack Gold (DWORD)",
    hackDiamonds = "💎 Hack Diamonds (FLOAT)",
    hackSpeed = "⚡ Speed Up Game",
    hackHealth = "❤️ Hack Health (freeze)",
    back = "↩️ Back",
    hackGoldSuccess = "💰 Gold hacked!",
    hackGoldFail = "⚠️ Not found.",
    hackDiamondSuccess = "💎 Diamonds increased!",
    hackDiamondFail = "⚠️ Not found.",
    hackSpeedSuccess = "⚡ Speed increased.",
    hackHealthSuccess = "❤️ Health freezed.",
    clearRAMSuccess = "🧹 RAM cleaned.",
    refreshGGSuccess = "♻️ Game Guardian refreshed.",
    infoText = [[
╔════════════════════════════╗
║        ℹ️ INFO             ║
╠════════════════════════════╣
║ 🔰 GG Script Pro UI v1     ║
║ 👤 Author: @Hieudzzzzcuto  ║
║ 🔄 Auto Update from Github ║
║ 📅 Date: 2025-08-04        ║
╚════════════════════════════╝
]],
    goodbye = "👋 Thanks for using!"
}

-- Biến lưu ngôn ngữ hiện tại
local currentLang = "vi"
local text = lang[currentLang]

-- Hàm chọn ngôn ngữ
function chooseLanguage()
    local choice = gg.choice(text.countryOptions, nil, text.chooseLang)
    if not choice then
        gg.alert(text.goodbye)
        os.exit()
    elseif choice == #text.countryOptions then
        return chooseLanguage()
    else
        -- Cơ bản, nếu chọn Việt Nam hoặc Back thì tiếng Việt, còn lại tiếng Anh
        if choice == 1 or choice == #text.countryOptions then
            currentLang = "vi"
        else
            currentLang = "en"
        end
        text = lang[currentLang]
        gg.toast(text.name .. " selected.")
    end
end

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

-- Yêu cầu nhập mật khẩu nếu chưa có
if not fileExists(file) then
  local input = gg.prompt({text.passPrompt}, {""})[1]
  if not input or input == "" then
    gg.alert(text.passEmpty)
    os.exit()
  end
  writePassword(input)
end

-- Đọc mật khẩu từ file và kiểm tra
local saved_pass = readPassword()
if saved_pass ~= correct_pass then
  gg.alert(text.passFail)
  os.exit()
end

gg.alert(text.passSuccess)

local CURRENT_VERSION = "1 beta"
local UPDATE_URL = "https://raw.githubusercontent.com/0908849165h/auto-update-/main/README.md"

-- Auto Update
function downloadUpdate()
    if not gg.makeRequest then
        gg.alert(text.noUpdateSupport)
        return
    end
    local resp = gg.makeRequest(UPDATE_URL)
    if not resp or resp.code ~= 200 then
        gg.toast(text.updateFail)
        return
    end
    local data = resp.content
    local newVer = data:match('CURRENT_VERSION%s*=%s*"(.-)"')
    if newVer and newVer ~= CURRENT_VERSION then
        local tmp = gg.getFile():gsub("%.lua$", "_updated.lua")
        local f = io.open(tmp, "w")
        f:write(data)
        f:close()
        gg.alert(string.format(text.updateNew, newVer))
        dofile(tmp)
        os.exit()
    else
        gg.toast(string.format(text.updateLatest, CURRENT_VERSION))
    end
end

-- Hiện logo
function showLogo()
    gg.alert(text.logo)
end

-- MENU CHÍNH
function mainMenu()
    local m = gg.choice({
        text.hackGame,
        text.cleanup,
        text.info,
        text.exit
    }, nil, text.menuTitle)

    if m == 1 then hackMenu() end
    if m == 2 then cleanupMenu() end
    if m == 3 then infoScript() end
    if m == 4 then exitScript() end
end

-- MENU HACK GAME
function hackMenu()
    local h = gg.choice({
        text.hackGold,
        text.hackDiamonds,
        text.hackSpeed,
        text.hackHealth,
        text.back
    }, nil, text.hackGame)
    if h == 1 then hackGold() end
    if h == 2 then hackDiamonds() end
    if h == 3 then hackSpeed() end
    if h == 4 then hackHealth() end
    if h == 5 then mainMenu() end
end

-- MENU DỌN DẸP
function cleanupMenu()
    local c = gg.choice({
        text.menuCleanup,
        "♻️ Refresh Game Guardian",
        text.back
    }, nil, text.cleanup)
    if c == 1 then clearRAM() end
    if c == 2 then refreshGG() end
    if c == 3 then mainMenu() end
end

-- CÁC HACK
function hackGold()
    gg.clearResults()
    gg.setRanges(gg.REGION_ANONYMOUS)
    gg.searchNumber("1000", gg.TYPE_DWORD)
    local r = gg.getResults(100)
    if #r > 0 then
        gg.editAll("999999", gg.TYPE_DWORD)
        gg.toast(text.hackGoldSuccess)
    else
        gg.alert(text.hackGoldFail)
    end
    mainMenu()
end

function hackDiamonds()
    gg.clearResults()
    gg.setRanges(gg.REGION_C_ALLOC)
    gg.searchNumber("5", gg.TYPE_FLOAT)
    local r = gg.getResults(50)
    if #r > 0 then
        gg.editAll("9999", gg.TYPE_FLOAT)
        gg.toast(text.hackDiamondSuccess)
    else
        gg.alert(text.hackDiamondFail)
    end
    mainMenu()
end

function hackSpeed()
    gg.setSpeed(3.0)
    gg.toast(text.hackSpeedSuccess)
    mainMenu()
end

function hackHealth()
    gg.clearResults()
    gg.searchNumber("100", gg.TYPE_FLOAT)
    local r = gg.getResults(30)
    if #r > 0 then
        for i, v in ipairs(r) do
            v.freeze = true
            v.value = "9999"
            v.freezeType = gg.FREEZE_NORMAL
        end
        gg.addListItems(r)
        gg.toast(text.hackHealthSuccess)
    else
        gg.alert(text.hackDiamondFail)
    end
    mainMenu()
end

function clearRAM()
    gg.clearResults()
    gg.toast(text.clearRAMSuccess)
    mainMenu()
end

function refreshGG()
    gg.setVisible(false)
    gg.clearResults()
    gg.toast(text.refreshGGSuccess)
    mainMenu()
end

function infoScript()
    gg.alert(text.infoText)
    mainMenu()
end

function exitScript()
    gg.alert(text.goodbye)
    os.exit()
end

-- Bắt đầu script
chooseLanguage()
showLogo()
downloadUpdate()

while true do
    if gg.isVisible(true) then
        gg.setVisible(false)
        mainMenu()
    end
end
