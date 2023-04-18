<template>
  <div class="main">
    <div class="cnt-block cnt-block--home-header">
      <h1>Value Cards</h1>
      <p>The Common Core Values Exercise</p>
    </div>

    <Timer />

    <Transition appear mode="out-in">

    <Home v-if="deckRound == 0" @start-round="roundUp" />
    
    <RoundOne v-else-if="deckRound == 1" :deckRound="deckRound" :cards="cards" @round-finished="roundUp"
      @push-to-round-one="pushOne" />
    
    <RoundTwo v-else-if="deckRound == 2" :deckRound="deckRound" :cards="roundOneImportant" @round-finished="roundUp"
      @push-to-round-two="pushTwo" />

    <RoundThree v-else-if="deckRound == 3" :deckRound="deckRound" :cards="roundTwoImportant" @round-finished="roundUp"
      @push-to-round-three="pushThree" />

    <Results v-else :cards="roundThreeImportant" @reset-deck="resetDeck" />

    </Transition>

  </div>
</template>
<script>
import Home from './views/Home.vue'
import RoundOne from './views/RoundOne.vue';
import RoundTwo from './views/RoundTwo.vue'
import RoundThree from './views/RoundThree.vue'
import Results from './components/Results.vue'
import Timer from './components/Timer.vue';

export default {
  name: 'App',
  components: {
    Home,
    RoundOne,
    RoundTwo,
    RoundThree,
    Results,
    Timer
  },
  methods: {
    roundUp() {
      this.deckRound++;
      console.log(this.deckRound)
    },
    pushOne(c) {
      this.roundOneImportant.push(c);
    },
    pushTwo(i) {
      this.roundTwoImportant.push(i);
      console.log(this.roundTwoImportant)
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
      cards: [
        { word: 'Empathy' },
        { word: 'Quiet' },
        { word: 'Risk' },
        { word: 'Appreciation' },
        { word: 'Parenting' },
        { word: 'Partnership' },
        { word: 'Faithfulness' },
        { word: 'Adventure' },
        { word: 'Contribution' },
        { word: 'Truth' },
        { word: 'Pleasure' },
        { word: 'Security' }
      ],
      roundOneImportant: [],
      roundTwoImportant: [],
      roundThreeImportant: []
    }
  }
}
</script>
<style lang="scss">

</style>