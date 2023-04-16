<template>
    <div class="roundone">
  
      <ButtonReset @reset-deck="resetDeck" :class="{hidden: !deckStarted}" />
        
      <div class="title">
        <h2>Round Two</h2>
      </div>      

      <CardCounter :roundOneImportant="roundOneImportant" :cardsViewed="cardsViewed" :class="{hidden: !deckStarted}" />
  
      <Cards v-if="cardsViewed < roundOneImportant.length" :roundOneImportant="roundOneImportant" :cardsViewed="cardsViewed" :deckStarted="deckStarted" @start-deck="startDeck" />
      
      <Controls @is-not-important="isNotImportant" @is-important="isImportant" @card-passed="cardPassed" :class="{hidden: !deckStarted}" />
      
      <ButtonNext :roundOneImportant="roundOneImportant" :cardsViewed="cardsViewed" @go-to-next="goToNext" />

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
        "roundOneImportant",
        "roundTwoImportant"
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
        this.roundTwoImportant.push(this.roundOneImportant[this.cardsViewed]); // approach to add to new deck
        this.cardsViewed++;
      },
      isNotImportant() {
        this.cardsViewed++;
      },
      cardPassed() {
        this.roundOneImportant.push(this.roundOneImportant.splice(this.roundOneImportant.indexOf(this.roundOneImportant[this.cardsViewed]), 1)[0]);
      },
      goToNext() {
        this.round = 3;
      }
    }
  }
  </script>
  <style>
  </style>