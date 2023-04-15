<template>
    <div class="roundone">
  
      <ButtonReset @reset-deck="resetDeck" :class="{hidden: !deckStarted}" />
        
      <div class="title">
        <h2>Round One</h2>
      </div>      

      <CardCounter :cards="cards" :cardsViewed="cardsViewed" :class="{hidden: !deckStarted}" />
  
      <ButtonNext :cards="cards" :cardsViewed="cardsViewed" @go-to-next="goToNext" />
  
      <Cards v-if="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" :deckStarted="deckStarted" @start-deck="startDeck" />
  
      <Results v-if="cardsViewed == cards.length" :roundOneImportant="roundOneImportant" />
  
      <Controls @is-not-important="isNotImportant" @is-important="isImportant" @card-passed="cardPassed" :class="{hidden: !deckStarted}" />
  
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
        "cards"
    ],
    data() {
        return {
            roundOneImportant: [],
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
    //   cardsViewed(val) {
    //     if (val == this.cards.length) {
    //       this.play = false;
    //     }
    //   }
    },
    methods: {
        startDeck() {
            this.deckStarted = true
            console.log('deck started')
        },
      resetDeck() {
        this.deckStarted = false
        this.cardsViewed = 0;
      },
      isImportant() {
        this.roundOneImportant.push(this.cards[this.cardsViewed]); // approach to add to new deck
        this.cardsViewed++;
      },
      isNotImportant() {
        this.cardsViewed++;
      },
      cardPassed() {
        this.cards.push(this.cards.splice(this.cards.indexOf(this.cards[this.cardsViewed]), 1)[0]);
        console.log('passed', this.cards) // QUESTION: why does this not need an $emit?
      },
      goToNext() {
        // this.stage++;
        // this.play = true;
      }
    }
  }
  </script>
  <style>
  </style>