<template>
  <div class="main">
    <Cards v-if="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" />
    <Results v-else :secondDeck="secondDeck" />
    <Controls :cards="cards" @card-removed="cardRemoved" @card-selected="cardSelected" @card-passed="cardPassed" />
  </div>
</template>
<script>
import Cards from './components/Cards.vue';
import Controls from './components/Controls.vue';
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: {
    Cards,
    Controls,
    Results
  },
  methods: {
    cardSelected() {
      this.secondDeck.push(this.cards[this.cardsViewed]);
      this.cardsViewed++;
    },
    cardPassed() {
      this.cards.push(this.cards.splice(this.cards.indexOf(this.cards[this.cardsViewed]), 1)[0]);
      console.log(this.cards)
    },
    cardRemoved() {
      this.cards[this.cardsViewed].removed == true
      this.cardsViewed++;
      console.log("bye bye")
    }
  },
  data() {
    return {
      cardsViewed: 0, // keep track of cards,
      secondDeck: [],
      cards: [
        {
          word: 'Courage',
          definition: 'This is obviously placeholder text for courage.',
          removed: false
        },
        {
          word: 'Strength',
          definition: 'This is the definition of the Strength. This is obviously placeholder text.',
          removed: false
        },
        {
          word: 'Love',
          definition: 'This is the definition of love.',
          removed: false
        },
        {
          word: 'Compassion',
          definition: 'Compassion is real, yall. This is obviously placeholder text.',
          removed: false
        }
      ]
    }    
  }
}
</script>
<style>
body {
  background-color: rgb(45, 45, 45);
}
.main {
  width: 500px;
  margin: 0 auto;
}
</style>