<template>
  <div class="main">
    <div class="cnt-block cnt-block--home-header">
      <h1>Value Cards</h1>
      <p>The Common Core Values Exercise</p>
    </div>

    <Transition appear mode="out-in">

      <Home v-if="deckRound == 0" @start-round="goToNext" />
      <DeckPlay v-else-if="deckRound == 1 && !results"
        :deckRound="deckRound"
        :cards="cards"
        @game-completed="gameCompleted"
        @go-to-next="goToNext"
        
        >{{ buttonMessage }}</DeckPlay>
      <DeckPlay v-else-if="deckRound == 2 && !results"
        :deckRound="deckRound"
        :cards="cards"
        @game-completed="gameCompleted"
        @go-to-next="goToNext"
        
        >{{ buttonMessage }}</DeckPlay>
      <DeckPlay v-else-if="deckRound == 3 && !results"
        :deckRound="deckRound"
        :cards="cards"
        @game-completed="gameCompleted"
        @go-to-next="goToNext"
        
        >{{ buttonMessage }}</DeckPlay>        

        <Results v-else-if="results" :cards="cards" @reset-deck="resetDeck" />
    </Transition>

    <!-- else show the results -->
    

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
  methods: {
    goToNext() {
      if (this.completed == true) {
        this.results = true;
        return;
      } else {
        this.deckRound++;
      }      
    },
    resetDeck() {
      this.deckRound = 0;
      this.complete = false;
      this.results = false;
    },
    gameCompleted() {
      this.completed = true;
    }
  },
  data() {
    return {
      deckRound: 0,
      completed: false,
      results: false,
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