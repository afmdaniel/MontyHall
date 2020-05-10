<template>
  <div id="app">
    <h1>Monty Hall Game Show!</h1>
    <div class="form">
      <div class="question" v-if="!started">
        <span>Number of doors:</span>
        <div class="doorAmount">{{doorAmount}}</div>
        <button class="btn-plus" @click="doorAmount++" style="margin-right:3px;">+</button>
        <button class="btn-sub" @click="doorAmount = doorAmount === 0? 0 : doorAmount - 1">-</button>
      </div>
      <div class="question" v-if="!started">
        <label for="giftDoor">Gift Door:</label>
        <input type="password" id="giftDoor" v-model.number="giftDoor" size="3" autocomplete="off" />
      </div>
      <button v-if="!started" @click="start">Start!</button>
      <div class="instruction" v-if="started">
        <p>INSTRUCTIONS</p>  
        <p><strong>Participant</strong>: Click on the door of your choice</p>
        <p><strong>Host</strong>: Click on the knob to open doors.</p>
      </div>
      <button v-if="started" @click="reset">Reset</button>
    </div>
    <div class="doors" v-if="started">
      <div v-for="i in doorAmount" :key="i">
        <Door
          :hasGift="i === giftDoor"
          :number="i"
          @select="selectDoor"
          :selected="i === selectedDoor"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Door from "./components/Door";

export default {
  name: "App",
  components: {
    Door
  },
  data: function() {
    return {
      started: false,
      doorAmount: 3,
      giftDoor: null,
      selectedDoor: null
    };
  },
  methods: {
    start: function() {
      this.started = true;
    },
    selectDoor: function(n) {
      this.selectedDoor = n;
    },
    reset: function() {
      Object.assign(this.$data, this.$options.data());
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}

body {
  color: #fff;
  background: linear-gradient(to right, rgb(21, 153, 87), rgb(21, 87, 153));
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

#app h1 {
  border: 1px solid #000;
  background-color: #0004;
  padding: 20px;
  margin-bottom: 30px;
}

.form {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 40px;
}

.question {
  font-size: 1.3rem;
  display: flex;
  justify-content: space-around;
  margin-bottom: 15px;
  width: 300px;
}

.instruction {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: 1.3rem;
  margin-bottom: 15px;
}

.instruction p {
  margin: 3px;
}

.btn-plus {
  background-color: rgb(21, 153, 87);
}

.btn-plus:active {
  background-color: rgb(13, 97, 55);
}

.btn-sub {
  background-color: rgb(21, 87, 153);
}

.btn-sub:active {
  background-color: rgb(20, 65, 109);
}

.doorAmount {
  margin: 0 15px;
}

.form button {
  font-size: 1.1rem;
  border: 1px solid;
  outline: none;
  border-radius: 10px;
}

.doors {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  align-self: stretch;
}

#giftDoor {
  background-color: teal;
  border: 1px solid;
  outline: none;
  border-radius: 10px;
  text-align: center;
  font-size: 1.1rem;
  font-weight: bolder;
}
</style>
