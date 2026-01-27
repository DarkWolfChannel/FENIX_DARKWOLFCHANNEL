var CHECK_TIME = 60;
var DELAY_BETWEEN_COMMANDS = 20;

var SCRIPT_RUNNING_FLAG = "MONEY_SCRIPT_RUNNING";
var wasRunning = GlobalVars.getBoolean(SCRIPT_RUNNING_FLAG);

if (wasRunning) {
    GlobalVars.putBoolean(SCRIPT_RUNNING_FLAG, false);
    var alreadySent = GlobalVars.getString("ALREADY_SENT") || "";
    var sessionSent = GlobalVars.getString("SESSION_SENT") || "";
    var totalCount = alreadySent.split(",").filter(function(n) { return n.trim() !== ""; }).length;
    var sessionCount = sessionSent.split(",").filter(function(n) { return n.trim() !== ""; }).length;
    
    Chat.log("§c╔════════════════╗");
    Chat.log("§c║ СТОП СКРИПТ   ║");
    Chat.log("§c╠════════════════╣");
    Chat.log("§fСессия: §e" + sessionCount);
    Chat.log("§fВсего: §e" + totalCount);
    
    var allSent = alreadySent.split(",").filter(function(n) { return n.trim() !== ""; });
    if (allSent.length > 0) {
        Chat.log("§fПоследние:");
        for (var i = Math.max(0, allSent.length - 3); i < allSent.length; i++) {
            Chat.log("§7• §f" + allSent[i]);
        }
    }
    
    Chat.log("§c╠════════════════╣");
    Chat.log("§fРестарт = запуск");
    Chat.log("§c╚════════════════╝");
    
    GlobalVars.putString("SESSION_SENT", "");
    throw "Stop";
} 
// --- ЗАПУСК СКРИПТА ---
else {
    GlobalVars.putBoolean(SCRIPT_RUNNING_FLAG, true);
    var running = true;
    var sentPlayers = [];
    var processingPlayers = {};
    var alreadySent = GlobalVars.getString("ALREADY_SENT") || "";
    GlobalVars.putString("SESSION_SENT", "");
    
    Chat.log("§a╔════════════════╗");
    Chat.log("§a║ ЗАПУСК СКРИПТА║");
    Chat.log("§a╠════════════════╣");
    Chat.log("§fПоиск: §e" + TWINK_NAME_START + "*");
    Chat.log("§fСумма: §e" + PAY_AMOUNT);
    Chat.log("§f2 команды через " + DELAY_BETWEEN_COMMANDS + " тиков");
    Chat.log("§a╠════════════════╣");
    Chat.log("§fРестарт = стоп");
    Chat.log("§a╚════════════════╝");
}

while (running) {
    if (!GlobalVars.getBoolean(SCRIPT_RUNNING_FLAG)) {
        running = false;
        break;
    }
    
    var players = World.getPlayers();
    var foundNew = false;
    
    for (var i = 0; i < players.length; i++) {
        if (!running) break;
        
        var player = players[i];
        var name = player.getName();
        name = name.replace(/§[0-9a-fk-or]/g, '');
        
        // Проверяем подходит ли ник
        if (name.startsWith(TWINK_NAME_START)) {
            var alreadySentList = alreadySent.split(",");
            var sentEver = alreadySentList.indexOf(name) !== -1;
            var isProcessing = processingPlayers[name];
            
            // Если НЕ отправляли и НЕ обрабатываем сейчас
            if (!sentEver && !isProcessing) {
                Chat.log("§a[💰] Найден: " + name);
                processingPlayers[name] = true; // БЛОКИРУЕМ сразу
                
                try {
                    // ПЕРВАЯ команда /pay
                    Chat.say("/pay " + name + " " + PAY_AMOUNT);
                    Client.waitTick(DELAY_BETWEEN_COMMANDS);
                    
                    if (!running) break;
                    
                    // ВТОРАЯ команда /pay
                    Chat.say("/pay " + name + " " + PAY_AMOUNT);
                    Client.waitTick(80); // Ждем завершения
                    
                    // Сохраняем факт отправки
                    sentPlayers.push(name);
                    alreadySent += name + ",";
                    GlobalVars.putString("ALREADY_SENT", alreadySent);
                    
                    var sessionSent = GlobalVars.getString("SESSION_SENT") || "";
                    sessionSent += name + ",";
                    GlobalVars.putString("SESSION_SENT", sessionSent);
                    
                    Chat.log("§a[✅] Отправлено " + name);
                    
                    Client.waitTick(150);
                    
                } catch(e) {
                    Chat.log("§c[✖] Ошибка: " + e);
                }
                
                foundNew = true;
                break; // Выходим из цикла по игрокам
            }
        }
    }
    
    // Если никого не нашли - ждем
    if (!foundNew) {
        Client.waitTick(CHECK_TIME);
    }
}

// --- ЗАВЕРШЕНИЕ ---
GlobalVars.putBoolean(SCRIPT_RUNNING_FLAG, false);
var alreadySentFinal = GlobalVars.getString("ALREADY_SENT") || "";
var sessionSentFinal = GlobalVars.getString("SESSION_SENT") || "";
var totalCount = alreadySentFinal.split(",").filter(function(n) { return n.trim() !== ""; }).length;
var sessionCount = sessionSentFinal.split(",").filter(function(n) { return n.trim() !== ""; }).length;

Chat.log("§c╔════════════════╗");
Chat.log("§c║ СТОП СКРИПТ   ║");
Chat.log("§c╠════════════════╣");
Chat.log("§fСессия: §e" + sessionCount);
Chat.log("§fВсего: §e" + totalCount);

var allSent = alreadySentFinal.split(",").filter(function(n) { return n.trim() !== ""; });
if (allSent.length > 0) {
    Chat.log("§fПоследние:");
    for (var i = Math.max(0, allSent.length - 3); i < allSent.length; i++) {
        Chat.log("§7• §f" + allSent[i]);
    }
}

Chat.log("§c╠════════════════╣");
Chat.log("§fРестарт = запуск");
Chat.log("§c╚════════════════╝");
GlobalVars.putString("SESSION_SENT", "");
