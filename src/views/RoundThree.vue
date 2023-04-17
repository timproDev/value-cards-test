<template>
    <div class="roundthree">
        
      <div class="title">
        <h2>Round Three</h2>
      </div>      

      <CardCounter :cards="cards" :cardsViewed="cardsViewed" :class="{hidden: !deckStarted}" />
      <Cards v-if="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" :deckStarted="deckStarted" @start-deck="startDeck" />
      <Controls @is-not-important="isNotImportant" @is-important="isImportant" @card-passed="cardPassed" :class="{hidden: !deckStarted}" />

    </div>
  </template>
  <script>
  import Cards from '../components/Cards.vue'
  import Controls from '../components/Controls.vue'
  import CardCounter from '../components/CardCounter.vue'
  export default {
    components: {
      Cards,
      Controls,
      CardCounter
    },
    props: [
        "cards"
    ],
    emits: [
      'push-to-round-three'
    ],
    data() {
        return {
            cardsViewed: 0, // keep track of cards,
            deckStarted: false
        }
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
        this.$emit('push-to-round-three',this.cards[this.cardsViewed]);
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