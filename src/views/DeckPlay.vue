<template>
  <div class="round-wrapper">

    <div class="title">
      <h2>Round {{ deckRound }}</h2>
    </div>

    <div :class="{ hidden: !deckStarted }">
      <p :class="cardsViewed < cards.length ? `show-this` : `hide-this`" class="number">
        <span>{{ cardsRemaining }}</span>
        cards remaining
      </p>
    </div>

    <Cards v-show="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" :deckStarted="deckStarted"
      @start-deck="startDeck" />

    <Controls v-if="deckStarted" :deckRound="deckRound" @is-not-important="isNotImportant" @is-important="isImportant"
      @card-passed="cardPassed" />

    <ButtonNext v-show="cardsViewed == cards.length" @go-to-next="goToNext">{{ buttonMessage }}
    </ButtonNext>

  </div>
</template>
<script>
import Cards from '../components/Cards.vue';
import Controls from '../components/Controls.vue';
import Results from '../components/Results.vue'
import ButtonNext from '../components/ButtonNext.vue'

export default {
  props: [
    "cards",
    "deckRound"
  ],
  emits: [
    'go-to-next',
    'game-completed'
  ],
  data() {
    return {
      cardsViewed: 0,
      deckStarted: false,
      buttonMessage: 'Go to next',
      completed: false
    }
  },
  components: {
    Cards,
    ButtonNext,
    Controls,
    Results
  },
  watch: {
    deckRound(v) {
      if (v == 1) {
        this.buttonMessage = "Go Round 2"
      } else if (v == 2) {
        this.buttonMessage = "Round 3 next"
      }
    },
    cards: {
      handler(val) {
        if (val.length - this.cardsViewed == 0) { // if this is the last card in deck, check complete criteria
          if (this.cards.length < 15) {
            this.endGame();
          }
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
    endGame() {
      this.buttonMessage = "Let's see your values"
      this.$emit('game-completed');
      this.deckStarted = false;
    },
    resetDeck() {
      this.deckStarted = false
      this.cardsViewed = 0;
    },
    isImportant() {
      this.cardsViewed++;
      if (this.cardsViewed == this.cards.length) { // if this is the lat card in deck, check complete criteria
        if (this.cards.length < 15) {
          this.endGame();
        }
        this.deckStarted = false;
      }
    },
    isNotImportant() {
      const removedItem = this.cards.indexOf(this.cards[this.cardsViewed]);
      if (removedItem > -1) {
        this.cards.splice(removedItem, 1);
      }
    },
    cardPassed() {
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
      this.$emit('go-to-next');
    }
  }
}
</script>
<style></style>