// ==UserScript==
// @name WoT-Leader Bot
// @namespace http://tampermonkey.net/
// @version 1.01
// @description wot-leader.ru BOT
// @author RAPOS
// @match https://wot-leader.ru/*
// @grant none
// ==/UserScript==

(function() {
    window.onload = function(){
        var TIMERINTERVAL = 30 * 1000; // ПЕРИОД ПРОВЕРКИ НА МОНЕТКИ (в милисекундах) !!!!!!!!!!!!!!!
        var clicks = 0;
        var profit = 0.00;

        var li = document.createElement("li");
        var t = document.createTextNode("Последний клик: 00:00:00 | Кликов: 0");
        li.id = "infoText";
        li.appendChild(t);
        document.getElementsByClassName("menu-top-personal")[0].firstElementChild.appendChild(li);

        var li2 = document.createElement("li");
        var t2 = document.createTextNode("Прибыль: 0.00");
        li2.id = "infoProfit";
        li2.style.color = "lime";
        li2.appendChild(t2);
        document.getElementsByClassName("menu-top-personal")[0].firstElementChild.appendChild(li2);

        var li3 = document.createElement("li");
        var t3 = document.createTextNode("Последняя монета: 0.00");
        li3.id = "infoLastGold";
        li3.style.color = "#ffbd00";
        li3.appendChild(t3);
        document.getElementsByClassName("menu-top-personal")[0].firstElementChild.appendChild(li3);

        var timerId = setInterval(function() {
            var d = new Date();
            var elcol = document.getElementsByTagName("div");
            for(var i = 0; i < elcol.length; i++)
            {
                if (elcol[i].style.bottom !== "" && elcol[i].style.bottom != "0") {
                    clicks++;
                    profit = (profit + parseFloat(elcol[i].innerText));
                    document.getElementById("infoText").innerText = "Последний клик: "+ d.getHours() +":"+ d.getMinutes() +":" +d.getSeconds() +" | Кликов: "+String(clicks);
                    document.getElementById("infoProfit").innerText = "Прибыль: " + profit.toFixed(2);
                    document.getElementById("infoLastGold").innerText = "Последняя монета: " + elcol[i].innerText;
                    elcol[i].click();
                }
            }
        }, TIMERINTERVAL);
    };
})();
