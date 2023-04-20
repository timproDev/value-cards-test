<template>
  <div class="round-wrapper">
      
    <div class="title">
      <h2>Round {{ deckRound }}</h2>
    </div>      

    <CardCounter :cards="cards" :cardsViewed="cardsViewed" :class="{hidden: !deckStarted}" />
    
    <Cards v-show="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" :deckStarted="deckStarted" @start-deck="startDeck" />
    
    <!-- <Timer v-if="deckStarted" :cardsViewed="cardsViewed" @times-up="cardPassed" /> -->
    
    <Controls v-if="deckStarted" :deckRound="deckRound" @is-not-important="isNotImportant" @is-important="isImportant" @card-passed="cardPassed" />
    
    <Transition name="apple">
      <ButtonNext v-show="cardsViewed == cards.length" @go-to-next="goToNext">Begin round 3</ButtonNext>
    </Transition>

  </div>
</template>
<script>
import Cards from '../components/Cards.vue';
import Controls from '../components/Controls.vue';
import Results from '../components/Results.vue'
import CardCounter from '../components/CardCounter.vue'
import ButtonNext from '../components/ButtonNext.vue'
import Timer from '../components/Timer.vue';

export default {
  props: [
      "cards",
      "deckRound"
  ],
  emits:[
    'round-finished',
    'push-to-important',
    'cards-finished'
  ],
  data() {
      return {
          cardsViewed: 0, // keep track of cards,
          deckStarted: false
      }
  },
  components: {
    Cards,
    ButtonNext,
    Controls,
    Results,
    CardCounter,
    Timer
  },
  watch: { // watch data for changes
    cardsViewed(val) {
      if (val == this.cards.length) {
         this.deckStarted = false;
         this.$emit('cards-finished');
      }
      // console.log('card viewed'), if card this.cardsViewed, restart timer
    }
  },
  methods: {
      startDeck() {
          this.deckStarted = true;
      },
    resetDeck() {
      this.deckStarted = false
      this.cardsViewed = 0;
    },
    isImportant() {
      console.log(this.cards[this.cardsViewed])
      if (this.deckRound == 1) {
        this.$emit('push-to-important',this.cards[this.cardsViewed]);
        this.cardsViewed++;
      } else {
        this.cardsViewed++; // leave the card in the important deck
      }       
    },
    isNotImportant() {
      console.log(this.cards[this.cardsViewed])
      if (this.deckRound == 1) {
        this.cardsViewed++;  
      } else {
        // remove from importnt deck
        // let removedItem = this.importantDeck.indexOf(this.cards.indexOf(this.cards[this.cardsViewed]));
        // if (removedItem > -1) {
        //   this.importantDeck.splice(removedItem, 1);
        // }
        // this.cardsViewed++;
        console.log("after splice",this.importantDeck)
      }        
    },
    cardPassed() {
      console.log(this.cards[this.cardsViewed])
      this.cards.push(this.cards.splice(this.cards.indexOf(this.cards[this.cardsViewed]), 1)[0]); // or use js .shift
    },
    goToNext() {
      this.$emit('round-finished');
    }
  }
}
</script>
<style>
</style>