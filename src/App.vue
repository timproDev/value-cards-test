<template>
  <div class="main">
    <div class="cnt-block cnt-block--home-header">
      <h1>Value Cards</h1>
      <p>The Common Core Values Exercise</p>
    </div>

    <Transition appear mode="out-in">

      <Home v-if="deckRound == 0" @start-round="roundUp" />
      <DeckPlay v-else-if="deckRound == 1"
        :deckRound="deckRound"
        :cards="cards"
        @game-completed="gameCompleted"
        @round-finished="roundUp"
        @cards-finished="cardsFinished"
        
        >{{ buttonMessage }}</DeckPlay>
      <DeckPlay v-else-if="deckRound == 2"
        :deckRound="deckRound"
        :cards="cards"
        @game-completed="gameCompleted"
        @round-finished="roundUp"
        @cards-finished="cardsFinished"
        
        >{{ buttonMessage }}</DeckPlay>
      <DeckPlay v-else-if="deckRound == 3"
        :deckRound="deckRound"
        :cards="cards"
        @game-completed="gameCompleted"
        @round-finished="roundUp"
        @cards-finished="cardsFinished"
        
        >{{ buttonMessage }}</DeckPlay>
      <Results v-else-if="completed == true" :cards="cards" @reset-deck="resetDeck" />

    </Transition>

  </div>
</template>
<script>
import Home from './views/Home.vue'
import DeckPlay from './views/DeckPlay.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: {
    Home,
    DeckPlay,
    Results
  },
  watch: {
    deckFinished(val) {
      console.log('deck finished!', val)
    },
    // deckRound(v) {
    //   if (v == 1) {
    //     this.buttonMessage = "Go Round 2"
    //   } else if (v == 2) {
    //     this.buttonMessage = "Round 3 next"
    //   } else if (v == 3) {
    //     this.buttonMessage = "Let's see your values"
    //   }
    // }
  },
  methods: {
    cardsFinished() {
      this.deckFinished = true;
    },
    roundUp() {
      // if game completed deckRound = completed, deckFinsihed = false
      this.deckRound++;
      this.deckFinished = false;
    },
    resetDeck() {
      this.deckRound = 0;
    },
    gameCompleted() {
      console.log("App says game completed")
    }
  },
  data() {
    return {
      deckRound: 0,
      completed: false,
      deckFinished: false,
      buttonMessage: '',
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