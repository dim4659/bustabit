# bustabit
//dim4659 scrip1
var     BaseBet = Math.round(engine.getBalance() / 100 / 13 - 0.5), // Base bet in bits. 1000 = 1000 bits.
        AutoCashout = 1.01; // Cashout. 2 means x2.0
        
var streaks = 0;
var bet = BaseBet;
var lastBet = 0;
var stbalance = engine.getBalance();
var profit = 0;
var profitproc = 0;
var d = new Date();
var StartTime = d.getTime();
var c = 0;
var d = 0;

engine.on('game_starting', function(info) {
       if(engine.lastGamePlay() == "LOST"){
            AutoCashout = 1.09;
            bet = bet * 12;
            if(bet = BaseBet * 12){
                d++;
                engine.placeBet(Math.round(bet)*100, Math.round(AutoCashout*100), function(){ });
            }
       }else
           if(engine.lastGamePlay() == "WON"){
              bet = Math.round(engine.getBalance() / 100 / 13 - 0.5);
              AutoCashout = 1.01;
              
           }
var newdate = new Date(); // функция времени
var timeplaying = ((newdate.getTime() - StartTime) / 1000) / 60; // узнаём время...
profitproc = ((engine.getBalance()-stbalance)*100/engine.getBalance()).toFixed(2);
profit = ((engine.getBalance()-stbalance)/100).toFixed(2)

if(streaks == 1){
        engine.placeBet(Math.round(bet)*100, Math.round(AutoCashout*100), function(){ });
        console.log(" bet  " + (bet));  
        c++;   
     }
console.log('прибыль: '+(profitproc)+'%  '+'профит: '+(profit)+' (в работе: ', Math.round(timeplaying), 'мин.)');
console.log("Нолей:  " + (c) + " Два ноля:  " + (d));     
});
 
engine.on('game_crash', function(data) {
        if(data.game_crash/100 < 1)
                streaks = 1;
        else
                streaks = 0;


});
