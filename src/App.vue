<template>
  <div id="app">
    <div>
      <p>Lets play Rock Paper Scissors</p>
      <div class="grid grid-cols-3">
        <div class="flex justify-center">
          <img @click="drawHand(1)" src="@/assets/1.png" class="w-20" alt="" />
        </div>
        <div class="flex justify-center">
          <img @click="drawHand(2)" src="@/assets/2.png" class="w-20" alt="" />
        </div>
        <div class="flex justify-center">
          <img @click="drawHand(0)" src="@/assets/0.png" class="w-20" alt="" />
        </div>
      </div>
      <div class="w-full flex justify-center">
        <div class="w-4/5 grid grid-cols-2">
          <div>
            <div>Your score {{ human }}</div>
            <div v-show="true">
              <div v-for="i in humanPickArray" :key="'human' + i.key">
                <p class="text-2xl" v-if="i.value == 0">
                  {{ hands[i.value] }}✊
                </p>

                <p class="text-2xl" v-if="i.value == 1">
                  {{ hands[i.value] }}🖐
                </p>
                <p class="text-2xl" v-if="i.value == 2">
                  {{ hands[i.value] }}✌️
                </p>
                <!-- <img :src="loadHuman(i.value)" alt="" /> -->
              </div>
            </div>
          </div>

          <div>
            <div>Compute score {{ computer }}</div>
            <div v-for="i in computerPickArray" :key="'computer' + i.key">
              <p class="text-2xl" v-if="i.value == 0">{{ hands[i.value] }}✊</p>

              <p class="text-2xl" v-if="i.value == 1">{{ hands[i.value] }}🖐</p>
              <p class="text-2xl" v-if="i.value == 2">{{ hands[i.value] }}✌️</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    // HelloWorld,
  },
  data() {
    return {
      hands: ["rock", "paper", "scissors"],
      computer: 0,
      human: 0,
      computerPick: null,
      humanPick: null,
      humanPickArray: [],
      computerPickArray: [],
      counter: 0,
      win: false,

      draw: false,
    };
  },
  methods: {
    loadHuman(j) {
      // console.log(j);
      return `@/assets/${j}.png`;
    },
    drawHand(event) {
      this.draw = true;
      this.computerPick = this.randomPicker();
      this.humanPick = event;
      let date = Date.now().toString();
      this.humanPickArray[date] = this.humanPick;
      let key = this.counter++;
      let value = this.humanPick;
      this.humanPickArray = [...this.humanPickArray, { key, value }];
      value = this.computerPick;
      this.computerPickArray = [...this.computerPickArray, { key, value }];
      //  hands: ["rock", "paper", "scissors"],
      if (this.humanPick == this.computerPick) {
        console.log("draw");
      } else if (
        (this.computerPick == 0 && this.humanPick == 1) ||
        (this.computerPick == 1 && this.humanPick == 2) ||
        (this.computerPick == 2 && this.humanPick == 0)
      ) {
        this.human++;
        console.log("human won");
      } else {
        this.computer++;
        console.log("computer won");
      }
    },
    randomPicker() {
      return Math.floor(Math.random() * 3);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
