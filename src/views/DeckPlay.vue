<template>
  <div class="round-wrapper">

    <div class="title">
      <h2>Round Title</h2>
      <button type="button" class="btn btn--back" @click.prevent="goBack">Back</button>
      <button type="button" class="btn btn--reset" @click.prevent="resetDeck">Restart</button>
    </div>

    <div v-show="!deckComplete">
      <p class="number">
        <span>{{ cardsRemaining }}</span>
        cards remaining
      </p>

    </div>

    <div v-show="!deckComplete" class="cards-wrapper">      
        <Card :cards="oneCard" :cardsViewed="cardsViewed" ref="childComp" />
    </div>

    <Controls v-show="!deckComplete" :deckRound="deckRound" @is-not-important="isNotImportant" @is-important="isImportant"
      @card-passed="cardPassed" />

    <ButtonNext v-show="deckComplete" @go-to-next="goToNext">{{ buttonMessage }}</ButtonNext>

    <Results v-show="results" :cards="cardDeck" @next-stage="nextStage" />

  </div>
</template>
<script>

import Card from '../components/Card.vue';
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
      gameEnded: false,
      results: false,
      cardsViewed: 0,
      deckRound: 1,
      deckComplete: false,
      buttonMessage: 'Go to next',
      roundOneImportant: [],
      roundTwoImportant: [],
      roundThreeImportant: []
    }
  },
  components: {
    Card,
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
      console.log('this.cardDeck', this.cardDeck);
      console.log('this.roundOneImportant', this.roundOneImportant);
      console.log('cards viwed', this.cardsViewed);
      // end the end of each deck,
      // shuffle them for the next round
      // and check if the game is over
      if (val == this.cardDeck.length) {
        // if, deck is done change state of deckComplete to true
        // remove last card from dom ************************************************************************************ - then comlete = true
        // get child card by key or ref amd remove from donw, this should active css transition, when finished, next expression fires - setTimeout?
        // console.log(this.$refs.childComp, "i think we done")
        this.deckComplete = true;
        // reset the deck
        this.cardsViewed = 0;
        
        // if on next round
        if (this.deckRound == 1) {
          // if (this.roundOneImportant.length < 10) {
          //   this.gameEnded = true;
          // }
        }
        if (this.deckRound == 2) {
          this.shuffleDeck(this.roundTwoImportant);
          // if (this.roundTwoImportant.length < 10) {
          //   this.gameEnded = true;
          // }
        }
        if (this.deckRound == 3) {
          this.shuffleDeck(this.roundThreeImportant);
          // if (this.roundThreeImportant.length < 10) {
          //   this.gameEnded = true;
          // }
        }
      }
    }
  },
  computed: {
    oneCard() {
      // if this.cardsViewed == this.cardDeck.length {

      // }
      return this.cardDeck[this.cardsViewed];
    },
    cardDeck() {
      if (this.deckRound == 1) {
        return this.cards;
      } else if (this.deckRound == 2) {
        return this.emptyDeck;
      } else if (this.deckRound == 3) {
        return this.roundTwoImportant;
      }
    },
    cardsRemaining() {
      return this.cardDeck.length - this.cardsViewed;
    }
  },
  methods: {
    goBack() {
      this.$emit('go-back');
    },
    resetDeck() {
      this.cardsViewed = 0;
      this.gameEnded = false;
      this.results = false;
      this.deckRound = 1;
      this.roundOneImportant = [];
      this.roundTwoImportant = [];
      this.roundThreeImportant = [];
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
        console.log('game over homie')
        return
      }
      this.deckRound++;
      this.deckComplete = false;
    },
    nextStage() {
      this.$emit('next-stage')
    }
  }
}
</script>
<style></style>