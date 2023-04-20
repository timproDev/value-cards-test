<template>
  <div class="main">
    <div class="cnt-block cnt-block--home-header">
      <h1>Value Cards</h1>
      <p>The Common Core Values Exercise</p>
    </div>
    <Transition appear mode="out-in">

      <Home v-if="deckRound == 0" @start-round="roundUp" />

      <RoundOne v-else-if="deckRound == 1" :deckRound="deckRound" :cards="cards" @round-finished="roundUp"
        @push-to-round-one="pushOne" @cards-finished="isDeckFinished" />

      <RoundTwo v-else-if="deckRound == 2" :deckRound="deckRound" :cards="roundOneImportant" @round-finished="roundUp"
        @push-to-round-two="pushTwo" />

      <RoundThree v-else-if="deckRound == 3" :deckRound="deckRound" :cards="roundTwoImportant" @round-finished="roundUp"
        @push-to-round-three="pushThree" />

      <Results v-else-if="this.completed == true" :cards="roundThreeImportant" @reset-deck="resetDeck" />

    </Transition>

  </div>
</template>
<script>
import Home from './views/Home.vue'
import RoundOne from './views/RoundOne.vue';
import RoundTwo from './views/RoundTwo.vue'
import RoundThree from './views/RoundThree.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: {
    Home,
    RoundOne,
    RoundTwo,
    RoundThree,
    Results
  },
  watch: {
    // roundOneImportant: {
    //   handler(val) {
    //     if ((val.length < 15 && val.length > 8) && (this.deckFinished == true)) {
    //       console.log("fits the criteria!")
    //     }
    //   },
    //   deep: true
    // },
    deckFinished(val) {
      if (
        (val == true) && (this.roundOneImportant.length < 15 && this.roundOneImportant.length > 8)
        ||
        (val == true) && (this.roundTwoImportant.length < 15 && this.roundTwoImportant.length > 8)
        ||
        (val == true) && (this.roundThreeImportant.length < 15 && this.roundThreeImportant.length > 8)
      ) {
        console.log("fits the criteria!")
        // this.completed = true;
      }
    }
  },
  methods: {
    isDeckFinished() {
      this.deckFinished = true;
    },
    roundUp() {
      this.deckRound++;
      this.deckFinished = false;
    },
    pushOne(c) {
      this.roundOneImportant.push(c);
    },
    pushTwo(i) {
      this.roundTwoImportant.push(i);
    },
    pushThree(c) {
      this.roundThreeImportant.push(c);
    },
    resetDeck() {
      this.deckRound = 0;
      this.roundOneImportant = [];
      this.roundTwoImportant = [];
      this.roundThreeImportant = [];
    }
  },
  data() {
    return {
      deckRound: 0,
      exerciseStarted: false,
      completed: false,
      deckFinished: false,
      cards: [
        { word: 'Empathy' },
        { word: 'Quiet' },
        { word: 'Risk' },
        { word: 'Appreciation' },
        { word: 'Parenting' },
        { word: 'Admiration' },
        { word: 'Spontaneity' },
        { word: 'Courage' },
        { word: 'Understanding' },
        { word: 'Pride' },
        { word: 'Rituals' },
        { word: 'Wealth' },
        { word: 'Sensuality' },
        { word: 'Justice' },
        { word: 'Trust' },
        { word: 'Discovery' },
        { word: 'Vitality' },
        { word: 'Feelings' },
        { word: 'Self-Control' },
        { word: 'Freedom' },
        { word: 'Kindness' },
        { word: 'Independence' },
        { word: 'Openness' }
      ],
      roundOneImportant: [],
      roundTwoImportant: [],
      roundThreeImportant: []
    }
  }
}
</script>
<style lang="scss"></style>