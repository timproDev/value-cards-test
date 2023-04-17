<template>
    <div class="roundtwo">
        
      <div class="title">
        <h2>Round Two</h2>
      </div>      

      <CardCounter :cards="cards" :cardsViewed="cardsViewed" :class="{hidden: !deckStarted}" />
      
      <Cards v-show="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" :deckStarted="deckStarted" @start-deck="startDeck" />
      
      <Controls :deckRound="deckRound" @is-not-important="isNotImportant" @is-important="isImportant" @card-passed="cardPassed" :class="{hidden: !deckStarted}" />
      
      <ButtonNext :cards="cards" :cardsViewed="cardsViewed" @go-to-next="goToNext">Begin round 3</ButtonNext>      
      
    </div>
  </template>
  <script>
  import Cards from '../components/Cards.vue'
  import Controls from '../components/Controls.vue'
  import CardCounter from '../components/CardCounter.vue'
  import ButtonNext from '../components/ButtonNext.vue'

  export default {
    components: {
      Cards,
      Controls,
      CardCounter,
      ButtonNext
    },
    props: [
        "cards",
        "deckRound"
    ],
    emits: [
      'push-to-round-two',
      'round-finished'
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
        this.$emit('push-to-round-two',this.cards[this.cardsViewed]);
        console.log('push-to-round-two',this.cards[this.cardsViewed])
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