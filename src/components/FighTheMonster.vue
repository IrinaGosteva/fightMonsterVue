<template>
  <div>
    <section class="row">
      <div cols="6" class="d-flex w-50 columns hero">
        <img src="" class="imgStyle" />
        <h1 class="text-center">You</h1>
        <div class="healthbar">
          <div class="heart"></div>
          <div
            class="healthbar text-center healthbarRed yourHealth"
            style=" color: white;"
            :style="{ width: yourHealth + '%' }"
          >{{ this.yourHealth }}</div>
        </div>
      </div>
      <div cols="6" class="d-flex w-50 columns hero">
        <img src="" class="imgStyle" />
        <h1 class="text-center">Monster</h1>
        <div class="healthbar">
          <div class="heart"></div>
          <div
            class="healthbar text-center healthbarRed"
            style="color: white;"
            :style="{ width: monsterHealth + '%' }" 
          >{{ this.monsterHealth }}</div>
        </div>
      </div>
    </section>
    <section class="row controls" v-if="show">
      <div class="small-12 columns small-text ">
        <button id="start-game" class="btn" @click="showChange">
          START NEW GAME
        </button>
      </div>
    </section>
    <section class="row controls small-text" v-else>
      <div class="small-12 columns">
        <button @click="attackAction" id="attack" class="btn">ATTACK</button>
        <button @click="specialAttackAction" id="special-attack" class="btn">
          SPECIAL ATTACK
        </button>
        <button @click="healAction" id="heal" class="btn">HEAL</button>
        <button @click="giveUpAction" id="give-up" class="btn">GIVE UP</button>
      </div>
    </section>
    <section class="row">
      <div class="small-12 columns fightTitle">
        <h1 v-if="youWon == true">You Won!!!</h1>
        <h1 v-else-if="youWon == false">You loose(((</h1>
        <ul>
          <li
            v-for="(totalValue, i) in totalValues"
            :key="totalValue"
          >
            {{ i }}: {{ totalValue }}
          </li>
        </ul>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "FighTheMonster",
  data: () => ({
    show: true,
    value: 0,
    classchange: "shrink",
    monsterHealth: 100,
    yourHealth: 100,
    totalValues: [],
    youWon: "start"
  }),
  watch: {
    monsterHealth: function() {
      if (this.monsterHealth <= 0) {
        this.show = true;
        this.youWon = 1;
      }
    },
    yourHealth: function() {
      if (this.yourHealth <= 0) {
        this.show = true;
        this.youWon = 0;
      }
    }
  },
  methods: {
    showChange: function() {
      this.show = false;
      this.yourHealth = 100;
      this.monsterHealth = 100;
      this.totalValues = [];
      this.youWon = "start";
    },
    attackAction: function() {
      this.yourHealth = this.yourHealth - Math.random().toFixed(1) * 5;
      this.monsterHealth = this.monsterHealth - Math.random().toFixed(1) * 5;
      this.totalValues.unshift("Monster hit you -" + this.yourHealth);
      this.totalValues.unshift("You hit the monster -" + this.monsterHealth);
    },
    specialAttackAction: function() {
      this.yourHealth = this.yourHealth - Math.random().toFixed(1) * 5;
      this.monsterHealth = this.monsterHealth - Math.random().toFixed(1) * 15;
      this.totalValues.unshift("Monster hit you -" + this.yourHealth);
      this.totalValues.unshift("You hit the monster with special attack -" + this.monsterHealth);
    },
    healAction: function() {
      this.yourHealth = this.yourHealth + Math.random().toFixed(1) * 5;
      this.yourHealth = this.yourHealth - Math.random().toFixed(1) * 5;
      this.totalValues.unshift("Monster hit you -" + this.yourHealth);
      this.totalValues.unshift("You heal yourself -" + this.yourHealth);
      if (this.yourHealth >= 100) {
        this.yourHealth = 100;
      }
    },
    giveUpAction: function() {
      this.yourHealth = 0;
      this.monsterHealth = 100;
    },
    stopEffect: function() {
      this.classchange = "shrink";
    },
    startEffect: function() {
      setInterval(() => {
        if (this.classchange == "shrink") {
          this.classchange = "highlight";
          console.log(this.classchange);
        } else {
          this.classchange = "shrink";
          console.log(this.classchange);
        }
      }, 5000);
    },
  },
  computed: {
    result: function() {
      return this.value > 37 ? "done" : this.value;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.text-center {
  text-align: center;
}
.healthbar {
  position: relative;
  height: 20px;
  background-color: #c7c7c7;
  margin: auto;
  transition: width 500ms;
  border-radius: 15px;
}
.healthbarRed {
  position: absolute;
  left: 0;
  width: 100%;
  background-color: #ff4037;
  margin: 0;
}
.controls,
.log {
  margin-top: 45px;
  text-align: center;
  padding: 10px;
  border: 0px solid #ccc;
  /* box-shadow: 0px 3px 6px #ccc; */
}
.turn {
  margin-top: 20px;
  margin-bottom: 20px;
  font-weight: bold;
  font-size: 22px;
}
.log ul {
  list-style: none;
  font-weight: bold;
  text-transform: uppercase;
}
.log ul li {
  margin: 5px;
}
.log ul .player-turn {
  color: blue;
  background-color: #e4e8ff;
}
.log ul .monster-turn {
  color: red;
  background-color: #ffc0c1;
}
button {
  font-size: 20px;
  background-color: #eee;
  padding: 15px;
  box-shadow: 0 1px 1px black;
  margin: 10px;
}
#start-game {
  background-color: #16bd21;
}
.btn {
  border: 1px solid white;
  border-radius: 30px;
  box-shadow: 2px 2px 20px gray;
}
#start-game:hover {
  background-color: #76ff7e;
}
#attack {
  background-color: #ff4939;
}
#attack:hover {
  background-color: #fb6c5f;
}
#special-attack {
  background-color: hsl(24, 96%, 52%);
}
#special-attack:hover {
  background-color: hsl(24, 95%, 59%);
}
#heal {
  background-color: #05ff15;
}
#heal:hover {
  background-color: #76ff7e;
}
#give-up {
  background-color: #9827f5;
}
#give-up:hover {
  background-color: #ac4ef8;
}
.hero {
  width: calc(50% - 40px);
  padding: 0 20px;
  display: inline-block;
}
.small-text * {
  font-size: 12px;
  font-weight: bold;
  color: white;
}
.heart {
  position: absolute;
  left: 0;
  display: inline-block;
  height: 20px;
  width: 20px;
  margin: -10px 0px;
  top: 55%;
  background-color: rgb(255, 35, 24);
  transform: rotate(-45deg);
  z-index: 10;
}
.heart:before,
.heart:after {
  content: "";
  position: absolute;
  height: 20px;
  width: 20px;
  background-color: rgb(255, 35, 24);
  border-radius: 50%;
  z-index: 10;
}
.heart:before {
  top: -10px;
  left: 0;
}
.heart:after {
  left: 10px;
  top: 0;
}
.imgStyle {
  display: inline-block;
  min-height: 120px;
  height: auto;
  width: 80%;
  background: aquamarine;
}
.fightTitle ul li {
  text-align: left;
  background: rgb(255, 141, 141);
  padding: 5px 15px;
  margin: 2px;
  list-style-type: none;
  
}
.fightTitle ul li:nth-child(odd) {
  text-align: left;
  background: rgb(155, 255, 205);
}
</style>
