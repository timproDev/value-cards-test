<template>
  <div class="round-wrapper">

    <div class="title">
      <h2>Round {{ deckRound }}</h2>
    </div>

    <div :class="{ hidden: !deckStarted }">
      <p :class="cardsViewed < cards.length ? `show-this` : `hide-this`" class="number"
      ><span>{{ cardsRemaining }}</span> cards remaining</p>
    </div>

    <Cards v-show="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" :deckStarted="deckStarted"
      @start-deck="startDeck" />

    <!-- <Timer v-if="deckStarted" :cardsViewed="cardsViewed" @times-up="cardPassed" /> -->

    <Controls v-if="deckStarted" :deckRound="deckRound" @is-not-important="isNotImportant" @is-important="isImportant"
      @card-passed="cardPassed" />

    <Transition name="apple">
      <ButtonNext v-show="cardsViewed == cards.length" @go-to-next="goToNext">Begin round 2</ButtonNext>
    </Transition>

  </div>
</template>
<script>
import Cards from '../components/Cards.vue';
import Controls from '../components/Controls.vue';
import Results from '../components/Results.vue'
import ButtonNext from '../components/ButtonNext.vue'
import Timer from '../components/Timer.vue';

export default {
  props: [
    "cards",
    "deckRound"
  ],
  emits: [
    'round-finished',
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
    Timer
  },
  watch: {
    cardsViewed(val) {
      if (val == this.cards.length) {
        this.deckStarted = false;
        this.$emit('cards-finished');
      }
    },
    cards: {
      handler(val) {
      if (val.length - this.cardsViewed == 0) {
        // console.log("watcher zero")
        this.deckStarted = false;
      }
      }, deep: true
    }
  },
  computed: {
    cardsRemaining() {
      return this.cards.length - this.cardsViewed;
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
      // keep it
      // iterate       
      this.cardsViewed++;
    },
    isNotImportant() {
      // delete it
      // iterate
      const removedItem = this.cards.indexOf(this.cards[this.cardsViewed]);
        if (removedItem > -1) {
          this.cards.splice(removedItem, 1);
        }
      // this.cardsViewed++;
      // console.log("NOT Important: cards length",this.cards.length)
      // console.log("NOT important: this.cardsViewed", this.cardsViewed)
    },
    cardPassed() {
      // push to bottom of deck
      // don't iterate
      this.cards.push(this.cards.splice(this.cards.indexOf(this.cards[this.cardsViewed]), 1)[0]);
    },
    shuffleDeck(a) {
      // Fisher-Yates
      var j, x, i;
      for (i = a.length - 1; i > 0; i--) {
        j = Math.floor(Math.random() * (i + 1));
        x = a[i];
        a[i] = a[j];
        a[j] = x;
      }
      return a;
    },
    goToNext() {
      this.$emit('round-finished');
    }
  }
}
</script>
<style></style>