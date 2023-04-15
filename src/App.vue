<template>
  <div class="main">

    <ButtonReset @reset-deck="resetDeck" />

    <CardCounter :cards="cards" :cardsViewed="cardsViewed" />

    <ButtonNext :cards="cards" :cardsViewed="cardsViewed" @go-to-next="goToNext" />

    <Cards v-if="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" />

    <Results v-if="cardsViewed == cards.length" :importantDeck="importantDeck" />

    <Controls v-show="play == true" @is-not-important="isNotImportant" @is-important="isImportant"
      @card-passed="cardPassed" />

  </div>
</template>
<script>
import Cards from './components/Cards.vue';
import Controls from './components/Controls.vue';
import Results from './components/Results.vue'
import CardCounter from './components/CardCounter.vue'
import ButtonNext from './components/ButtonNext.vue'
import ButtonReset from './components/ButtonReset.vue'

export default {
  name: 'App',
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
        this.play = false;
      }
    }
  },
  methods: {
    resetDeck() {
      this.cardsViewed = 0;
      this.stage = 1;
      this.play = true;
    },
    isImportant() {
      this.importantDeck.push(this.cards[this.cardsViewed]); // approach to add to new deck
      this.cardsViewed++;
    },
    isNotImportant() {
      this.cardsViewed++;
    },
    cardPassed() {
      this.cards.push(this.cards.splice(this.cards.indexOf(this.cards[this.cardsViewed]), 1)[0]);
    },
    goToNext() {
      this.stage++;
      this.play = true;
    }
  },
  data() {
    return {
      cardsViewed: 0, // keep track of cards
      play: true,
      stage: 1,
      importantDeck: [],
      cards: [
        {
          word: 'Accountability',
          important: true
        },
        {
          word: 'Achievement',
          important: true
        },
        {
          word: 'Teamwork',
          important: true
        },
        {
          word: 'Thrift',
          important: true
        },
        {
          word: 'Time',
          important: true
        }
      ]
    }
  }
}
</script>
<style lang="scss">
body {
  font-family: 'Nunito', sans-serif;
  background-color: #D6D6D6;
}

.main {
  width: 400px;
  margin: 0 auto;
}
.number {
  text-align: center;
}
.controls {
  display: flex;
  flex-direction: row;
  column-gap: 16px;
  padding: 24px;
  justify-content: center;
  margin-top: 3rem;
}

button,
.btn {
  position: relative;
  display: inline-flex;
  text-decoration: none;
  font-weight: bold;
  align-items: center;
  justify-content: center;
  //
  background-color: #fff;
  border: none;
  outline: none;
  height: 120px;
  cursor: pointer;
  border-radius: 160px;
  width: 80px;
  height: 80px;
  transition: all 120ms linear;

  &:hover {
    background-color: aqua;
  }
}

.btn--reset {
  width: auto;
  background-color: transparent;
  border: none;
  text-decoration: underline;
  display: inline;
  height: auto;
  padding: 1rem 0;
}

.hide-this {
  visibility: hidden;
  opacity: 0;
}

.card {
  border-radius: 8px;
  background-color: #F4F4F4;
  color: #454545;
  border: 16px solid #FCFCFC;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 210px;
  justify-content: center;
  align-content: center;
  box-shadow:
    0px 2.8px 2.2px rgba(0, 0, 0, 0.02),
    0px 6.7px 5.3px rgba(0, 0, 0, 0.028),
    0px 12.5px 10px rgba(0, 0, 0, 0.035);

  h3 {
    font-size: 36px;
  }
}
</style>