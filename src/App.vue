<script setup>
import { ref, reactive } from "vue";
const namePlayer1 = ref("ArtemDefault");
const namePlayer2 = ref("NickDefault");
const namePlayer3 = ref("MaryDefault");

const gameStand = ref("");

const personWhoDraw = ref(0);
const prsonsDraw = reactive([
  {
    name: namePlayer1,
    draw: "Elephant",
  },
  {
    name: namePlayer2,
    draw: "Banana",
  },
  {
    name: namePlayer3,
    draw: "Pinapple",
  },
]);

const onStartbtnClick = () => {
  return (gameStand.value = "started");
};
const onFirstPlayerBtn = () => {
  return (gameStand.value = "show_what_to_draw");
};
const onNextBtnClick = () => {
  if (personWhoDraw.value === prsonsDraw.length - 1) {
    personWhoDraw.value = 0;
    return (gameStand.value = "end");
  } else if (personWhoDraw.value !== prsonsDraw.length) {
    return personWhoDraw.value++;
  }
};
const onClickResetGame = () => {
  namePlayer1.value = "";
  namePlayer2.value = "";
  namePlayer3.value = "";
  return (gameStand.value = "");
};
</script>

<template>
  <div v-show="gameStand === ''">
    <h1>players</h1>
    <div class="inputs-wrap">
      <input
        v-model="namePlayer1"
        type="text"
        name="pl1"
        id="pl1"
        placeholder="Player 1"
      />
    </div>
    <div class="inputs-wrap">
      <input
        v-model="namePlayer2"
        type="text"
        name="pl2"
        id="pl2"
        placeholder="Player 2"
      />
    </div>
    <div class="inputs-wrap">
      <input
        v-model="namePlayer3"
        type="text"
        name="3"
        id="pl3"
        placeholder="Player 3"
      />
    </div>
    <button
      type="button"
      @click="onStartbtnClick"
    >
      Start game
    </button>
  </div>
  <div v-show="gameStand == 'started'">
    <div class="playerone">
      <h3>{{ prsonsDraw[personWhoDraw].name }}</h3>
      <button
        type="button"
        @click="onFirstPlayerBtn"
      >
        Show
      </button>
    </div>
  </div>
  <div v-show="gameStand == 'show_what_to_draw'">
    <p>
      Player name: <b>{{ prsonsDraw[personWhoDraw].name }}</b>
    </p>
    <p>
      Player draw: <b>{{ prsonsDraw[personWhoDraw].draw }}</b>
    </p>
    <button
      type="button"
      @click="onNextBtnClick"
    >
      <span v-if="personWhoDraw !== prsonsDraw.length - 1">Next player</span>
      <span v-else>Game ended</span>
    </button>
    {{}}
  </div>
  <div v-show="gameStand == 'end'">
    <h3>Game end!</h3>
    <button
      type="button"
      @click="onClickResetGame"
    >
      Play Again!
    </button>
  </div>
</template>

<style scoped>
.inputs-wrap {
  display: block;
}
button {
  display: block;
}
</style>
