<template>
  <div class="main">
    <div class="cnt-block cnt-block--home-header">
      <h1>Value Cards</h1>
      <p>The Common Core Values Exercise</p>
    </div>
    <Transition appear mode="out-in">

      <Home v-if="deckRound == 0" @start-round="roundUp" />

      <DeckPlay v-else-if="deckRound == 1" :deckRound="deckRound" :cards="cards" @round-finished="roundUp" @cards-finished="isDeckFinished" />

      <DeckPlay v-else-if="deckRound == 2" :deckRound="deckRound" :cards="cards" @round-finished="roundUp" @cards-finished="isDeckFinished" />

      <DeckPlay v-else-if="deckRound == 3" :deckRound="deckRound" :cards="cards" @round-finished="roundUp" @cards-finished="isDeckFinished" />

      <Results v-else-if="this.completed == true" :cards="roundThreeImportant" @reset-deck="resetDeck" />

    </Transition>

  </div>
</template>
<script>
import Home from './views/Home.vue'
import DeckPlay from './views/DeckPlay.vue'
import RoundThree from './views/RoundThree.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: {
    Home,
    DeckPlay,
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
      console.log('deck finished!', val)
      // if (
      //   (val == true) && (this.roundOneImportant.length < 15 && this.roundOneImportant.length > 8)
      //   ||
      //   (val == true) && (this.roundTwoImportant.length < 15 && this.roundTwoImportant.length > 8)
      //   ||
      //   (val == true) && (this.roundThreeImportant.length < 15 && this.roundThreeImportant.length > 8)
      // ) {
        
        // this.completed = true;
      //}
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
    pushImportant(c) {
      this.importantDeck.push(c);
      console.log('important deck includes:', this.importantDeck)
    },
    resetDeck() {
      this.deckRound = 0;
      this.importantDeck = [];
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
      importantDeck: []
    }
  }
}
</script>