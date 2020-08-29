<template>
<div>
    <div style="position: absolute; left:10%; top:32%; width:300px;">
        <div class="progress">
            <div class="progress-bar  bg-danger" role="progressbar" aria-valuenow="{{rino[0].hp}}" aria-valuemin="0" aria-valuemax="300" v-bind:style="userHpBar">{{rino[0].hp}}</div>
        </div>
        <img :src="rino[0].src" alt="Rino">
    </div>
    <div style="position: absolute; right:20%; top:32%; width:300px;">
        <div class="progress">
            <div class="progress-bar bg-danger" role="progressbar" aria-valuenow="{{kyaru[0].hp}}" aria-valuemin="0" aria-valuemax="500" v-bind:style="opponentHpBar">{{kyaru[0].hp}}</div>
        </div>
        <img :src="kyaru[0].src" alt="Kyaru">
    </div>
    <div style="position: absolute; width:500px; height:300px; border: solid 1px #FFFFFF; top:55%; right:40%; background-color:lightblue;">
        <p>{{battleText}}</p>
        <div v-if="fightOn">
            <button @click="processAttack(1)" style="width:300px; height:40px; border: solid 1px #FFFFFF; " class="btn btn-primary">Attack</button>
            <button @click="processAttack(2)" style="width:300px; height:40px; border: solid 1px #FFFFFF; ;" class="btn btn-danger">Special Attack</button>
        </div>
        <div v-if="defOn">
            <button @click="processDef()" style="width:300px; height:40px; border: solid 1px #FFFFFF; ;" class="btn btn-danger">Defend</button>
        </div>
        <div v-if="endOn">
            <button @click="processEnd()" style="width:300px; height:40px; border: solid 1px #FFFFFF; " class="btn btn-primary">OK</button>
        </div>
    </div>

</div>
</template>

<script>
export default {
    data: function () {
        return {
            kyaru: [{
                name: "Kyaru",
                hp: 500,
                src: require("../assets/Kayle.png")
            }, ],
            rino: [{
                name: "Rino ",
                hp: 300,
                src: require("../assets/Rino.png")
            }, ],
            userHpBar: {
                width: "100%"
            },
            userFill: 100,
            opponentHpBar: {
                width: "100%"
            },
            opponentFill: 100,
            userDamage: 0,
            opponentDamage: 0,
            defOn: false,
            fightOn: true,
            endOn: false,
            battleText: "จงทำให้ HP ของ Kyaru หมดก่อนที่ HP เราจะหมด",
            kyaruAtk: 0,
            rinoAtk: 0,
        };

    },
    methods: {
        processAttack: function (option) {
            switch (option) {
                case 1:
                    //generate random number
                    var random = Math.floor((Math.random() * 100) + 50);
                    //do damage to kyaru
                    this.rinoAtK = random;
                    this.kyaru[0].hp -= this.rinoAtK;
                    this.opponentFill -= this.rinoAtK / 5;
                    this.opponentHpBar.width = this.opponentFill + "%"
                    if (this.kyaru[0].hp <= 0) {
                        this.opponentHpBar.width = "0%"
                        this.battleText = "You win! Play again?";
                        this.endOn = true;
                        this.fightOn = false;
                        this.defOn = false;
                    } else if (this.kyaru[0].hp > 0) {
                        //continue battle
                        this.battleText = "You did damage" + random + "! but Kayru will attacking you";
                        this.fightOn = false;
                        this.defOn = true;
                    }
                    break;
                case 2:
                    //generate random number
                    var randomS = Math.floor((Math.random() * 150) + 70);
                    //do damage to kyaru
                    this.rinoAtK = randomS;
                    this.kyaru[0].hp -= this.rinoAtK;
                    this.opponentFill -= this.rinoAtK / 5;
                    this.opponentHpBar.width = this.opponentFill + "%"
                    if (this.kyaru[0].hp <= 0) {
                        this.opponentHpBar.width = "0%"
                        this.battleText = "You win! Play again?";
                        this.endOn = true;
                        this.fightOn = false;
                        this.defOn = false;
                    } else if (this.kyaru[0].hp > 0) {
                        //continue battle
                        this.battleText = "You did damage" + randomS + "! but Kayru will attacking you";
                        this.fightOn = false;
                        this.defOn = true;
                    }
                    break;
            }
        },
        processDef: function () {
            //generate random number
            var random = Math.floor((Math.random() * 100) + 20);
            //do damage to kyaru
            this.kyaruAtk = random;
            this.rino[0].hp -= this.kyaruAtk;
            this.userFill -= this.kyaruAtk / 3;
            this.userHpBar.width = this.opponentFill + "%"
            if (this.rino[0].hp <= 0) {
                this.userHpBar.width = "0%"
                this.battleText = "You lose! Play again?";
                this.endOn = true;
                this.fightOn = false;
                this.defOn = false;
            } else if (this.rino[0].hp > 0) {
                //continue battle
                this.battleText = "You got damaged" + random + "!";
                this.fightOn = true;
                this.defOn = false;
            }
        },
        processEnd: function () {
            //reset data to start new game
            this.endOn = false;
            this.fightOn = true;
            this.defOn = false;
            this.battleText = "จงทำให้ HP ของ Kyaru หมดก่อนที่ HP เราจะหมด"
            this.userFill = 100
            this.opponentFill = 100
            this.userHpBar.width = "100%"
            this.opponentHpBar.width = "100%"
            this.kyaru[0].hp = 500
            this.rino[0].hp = 300
        }

    }

};
</script>

<style>
body {
    background-image: url("../assets/bg.png");
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: 100% 100%;
}
</style>
