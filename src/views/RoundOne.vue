<template>
    <div class="roundone">
  
      <!-- <ButtonReset @reset-deck="resetDeck" :class="{hidden: !deckStarted}" /> -->
        
      <div class="title">
        <h2>Round One</h2>
      </div>      

      <CardCounter :cards="cards" :cardsViewed="cardsViewed" :class="{hidden: !deckStarted}" />
  
      <Cards v-if="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" :deckStarted="deckStarted" @start-deck="startDeck" />
      
      <Controls :roundIt="roundIt" @is-not-important="isNotImportant" @is-important="isImportant" @card-passed="cardPassed" :class="{hidden: !deckStarted}" />
      
      <ButtonNext :cards="cards" :cardsViewed="cardsViewed" @go-to-next="goToNext" />

    </div>
  </template>
  <script>
  import Cards from '../components/Cards.vue';
  import Controls from '../components/Controls.vue';
  import Results from '../components/Results.vue'
  import CardCounter from '../components/CardCounter.vue'
  import ButtonNext from '../components/ButtonNext.vue'
  import ButtonReset from '../components/ButtonReset.vue'
  
  export default {
    props: [
        "cards",
        "roundIt"
    ],
    emits:['round-finished', 'push-to-round-one'],
    data() {
        return {
            cardsViewed: 0, // keep track of cards,
            deckStarted: false
        }
    },
    components: {
      Cards,
      ButtonNext,
      ButtonReset,
      Controls,
      Results,
      CardCounter
    },
    watch: { // watch data for changes
      cardsViewed(val) {
        if (val == this.cards.length) {
           this.deckStarted = false;
        }
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
        this.$emit('push-to-round-one',this.cards[this.cardsViewed]);
        this.cardsViewed++;
      },
      isNotImportant() {
        this.cardsViewed++;
      },
      cardPassed() {
        this.cards.push(this.cards.splice(this.cards.indexOf(this.cards[this.cardsViewed]), 1)[0]);
      },
      goToNext() {
        this.$emit('round-finished');
      }
    }
  }
  </script>
  <style>
  </style>