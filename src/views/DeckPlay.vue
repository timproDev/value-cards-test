<template>
  <div class="round-wrapper" :class="roundStyle">

    <div class="title">
      <h2>Round {{ deckRound }}</h2>
      <button type="button" class="btn btn--back" @click.prevent="goBack">Back</button>
      <button type="button" class="btn btn--reset" @click.prevent="resetDeck">Restart</button>
    </div>

    <Transition>

      <div v-show="!deckComplete">

        <p class="number">
          <span>{{ cardsRemaining }}</span>
          cards remaining
        </p>

        <Cards :deckComplete="deckComplete" :cards="oneCard" :cardsViewed="cardsViewed" />

        <Controls :deckComplete="deckComplete" :deckRound="deckRound" @is-not-important="isNotImportant"
          @is-important="isImportant" @card-passed="cardPassed" />

      </div>

    </Transition>


    <Transition name="apple">
      <ButtonNext v-show="showNextBtn && !results" @go-to-next="goToNext">{{ buttonMessage }}</ButtonNext>
    </Transition>

    <Transition name="apple">
      <Results v-show="results" :cards="resultsDeck" @next-stage="nextStage" />
    </Transition>


  </div>
</template>
<script>
import Cards from '../components/Cards.vue';
import Controls from '../components/Controls.vue';
import ButtonNext from '../components/ButtonNext.vue';
import Results from '../components/Results.vue';

export default {
  props: [
    "cards"
  ],
  emits: [
    'go-to-next',
    'next-stage',
    'go-back'
  ],
  data() {
    return {
      enoughCards: 5, // 4 is snough
      gameEnded: false,
      deckComplete: true,
      cardsViewed: 0,
      deckRound: 1,
      showNextBtn: false,
      results: false,
      buttonMessage: 'Go to next',
      roundOneImportant: [],
      roundTwoImportant: [],
      roundThreeImportant: []
    }
  },
  components: {
    Cards,
    ButtonNext,
    Controls,
    Results
  },
  watch: {
    gameEnded(bool) {
      if (bool) {
        this.buttonMessage = "See results"
      }
    },
    cardsViewed(val) {
      if (val == this.cardDeck.length) {
        this.deckComplete = true;
        setTimeout(() => {
          this.showNextBtn = true;
        }, 500);
        if (this.deckRound == 1) {
          if (this.roundOneImportant.length < this.enoughCards) {
            this.gameEnded = true;
          }
        }
        if (this.deckRound == 2) {
          this.shuffleDeck(this.roundTwoImportant);
          if (this.roundTwoImportant.length < this.enoughCards) {
            this.gameEnded = true;
          }
        }
        if (this.deckRound == 3) {
          this.shuffleDeck(this.roundThreeImportant);
          if (this.roundThreeImportant.length < this.enoughCards) {
            this.gameEnded = true;
          }
        }
      }
    }
  },
  mounted() {
    this.deckComplete = false;
  },
  computed: {
    oneCard() {
      return this.cardDeck[this.cardsViewed];
    },
    resultsDeck() {
      if (this.deckRound == 1) {
        return this.roundOneImportant;
      } else if (this.deckRound == 2) {
        return this.roundTwoImportant;
      } else if (this.deckRound == 3) {
        return this.roundThreeImportant;
      }
    },
    cardDeck() {
      if (this.deckRound == 1) {
        return this.cards;
      } else if (this.deckRound == 2) {
        return this.roundOneImportant;
      } else if (this.deckRound == 3) {
        return this.roundTwoImportant;
      }
    },
    cardsRemaining() {
      return this.cardDeck.length - this.cardsViewed;
    },
    roundStyle() {
      if (this.deckRound == 1) {
        return 'round-style-1';
      } else if (this.deckRound == 2) {
        return 'round-style-2';
      } else if (this.deckRound == 3) {
        return 'round-style-3';
      }
    },
  },
  methods: {
    goBack() {
      this.$emit('go-back');
    },
    resetDeck() {
      this.deckComplete = true;
      setTimeout(() => {
        this.deckComplete = false;
        this.cardsViewed = 0;
        this.showNextBtn = false;
        this.gameEnded = false;
        this.results = false;
        this.deckRound = 1;
        this.roundOneImportant = [];
        this.roundTwoImportant = [];
        this.roundThreeImportant = [];
      }, 700)
    },
    isImportant() {
      if (this.deckRound == 1) {
        this.roundOneImportant.push(this.cardDeck[this.cardsViewed]);
      } else if (this.deckRound == 2) {
        this.roundTwoImportant.push(this.cardDeck[this.cardsViewed]);
      } else if (this.deckRound == 3) {
        this.roundThreeImportant.push(this.cardDeck[this.cardsViewed]);
      }
      this.cardsViewed++;
    },
    isNotImportant() {
      this.cardsViewed++;
    },
    cardPassed() {
      this.cardDeck.push(this.cardDeck.splice(this.cardDeck.indexOf(this.cardDeck[this.cardsViewed]), 1)[0]);
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
      if (this.gameEnded) {
        this.results = true;
        return
      }
      this.showNextBtn = false;
      // let button fade away then reset
      setTimeout(() => {
        this.deckComplete = false;
        this.cardsViewed = 0;
        this.deckRound++;
      }, 300);
    },
    nextStage() {
      this.$emit('next-stage')
    }
  }
}
</script>
<style></style>