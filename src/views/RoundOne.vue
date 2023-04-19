<template>
    <div class="round-wrapper">
        
      <div class="title">
        <h2>Round One</h2>
      </div>      

      <CardCounter :cards="cards" :cardsViewed="cardsViewed" :class="{hidden: !deckStarted}" />
      
      <Cards v-show="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" :deckStarted="deckStarted" @start-deck="startDeck" />
      
      <Timer v-if="deckStarted" :cardsViewed="cardsViewed" @times-up="cardPassed" />
      
      <Controls v-if="deckStarted" :deckRound="deckRound" @is-not-important="isNotImportant" @is-important="isImportant" @card-passed="cardPassed" />
      
      <Transition name="apple">
        <ButtonNext v-show="cardsViewed == cards.length" @go-to-next="goToNext">Begin round 2</ButtonNext>
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
      Controls,
      Results,
      CardCounter,
      Timer
    },
    watch: { // watch data for changes
      cardsViewed(val) {
        if (val == this.cards.length) {
           this.deckStarted = false;
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
        this.$emit('push-to-round-one',this.cards[this.cardsViewed]);
        this.startTimer = true;
        this.cardsViewed++;
      },
      isNotImportant() {
        this.startTimer = true;
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