<template>
  <div class="main">
    <div class="cnt-block cnt-block--home-header">
      <h1>Value Cards</h1>
      <p>The Common Core Values Exercise</p>
    </div>

    <Home v-if="deckRound == 0" @start-round="roundUp" />

    <RoundOne v-else-if="deckRound == 1" :deckRound="deckRound" :cards="cards" @round-finished="roundUp"
      @push-to-round-one="pushOne" />

    <RoundTwo v-else-if="deckRound == 2" :deckRound="deckRound" :cards="roundOneImportant" @round-finished="roundUp"
      @push-to-round-two="pushTwo" />

    <RoundThree v-else-if="deckRound == 3" :deckRound="deckRound" :cards="roundTwoImportant" @round-finished="roundUp"
      @push-to-round-three="pushThree" />

    <Results v-else :cards="roundThreeImportant" @reset-deck="resetDeck" />

  </div>
</template>
<script>
import Home from './views/Home.vue'
import RoundOne from './views/RoundOne.vue';
import RoundTwo from './views/RoundTwo.vue'
import RoundThree from './views/RoundThree.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: {
    Home,
    RoundOne,
    RoundTwo,
    RoundThree,
    Results
  },
  methods: {
    roundUp() {
      this.deckRound++;
      console.log(this.deckRound)
    },
    pushOne(c) {
      this.roundOneImportant.push(c);
    },
    pushTwo(i) {
      this.roundTwoImportant.push(i);
      console.log(this.roundTwoImportant)
    },
    pushThree(c) {
      this.roundThreeImportant.push(c);
    },
    resetDeck() {
      this.deckRound = 0;
      this.roundOneImportant = [];
      this.roundTwoImportant = [];
      this.roundThreeImportant = [];
    }
  },
  data() {
    return {
      deckRound: 0,
      cards: [
        { word: 'Empathy' },
        { word: 'Quiet' },
        { word: 'Risk' },
        { word: 'Appreciation' },
        { word: 'Parenting' },
        { word: 'Admiration' },
        { word: 'Surrender' },
        { word: 'Action' },
        { word: 'Excellence' },
        { word: 'Inspiration' },
        { word: 'Fairness' },
        { word: 'Partnership' },
        { word: 'Faithfulness' },
        { word: 'Adventure' },
        { word: 'Contribution' },
        { word: 'Truth' },
        { word: 'Pleasure' },
        { word: 'Security' }
      ],
      roundOneImportant: [],
      roundTwoImportant: [],
      roundThreeImportant: []
    }
  }
}
</script>
<style lang="scss">
:root {
  --color-primary: rgb(0, 37, 202);
}
body {
  font-family: 'Questrial', sans-serif;
  background-color: #363636;
}

.main {
  width: 400px;
  margin: 0 auto;
  padding: 2rem;
  background-color: #D6D6D6;
  border-radius: 2px;
}

.cnt-block {
  $this: &;

  h1,h2,h3,h4,h5,h6 {
    margin: 0;
    padding: 0;
  }
  p, li, li p, span {
    margin: 0;
    padding: 0;
  }
  &--home-hero {
    text-align: center;
    padding: 2rem;    
  }
  &--home-header {
    text-align: center;
    padding: 2rem;
    border-bottom: 1px dashed #adadad;
  }
}
.header {

  h1,
  p {
    margin: 0;
    padding: 0;
    text-align: center;
  }
}

.title {
  h2 {
    margin: 0;
    padding: 1rem 0;
    text-align: center;
  }
}

.number {
  padding-top: 0;
  text-align: center;
  line-height: 26px;
  color:#616161;
  
  span {
    display: inline-block;
    background-color: #fff;
    border-radius: 100px;
    width: 24px;
    height: 24px;
    color: var(--color-primary);
    font-weight: bold;
  }
}

.controls-wrapper {
    padding: 2rem 0;
    text-align: center;
    border-bottom: 1px dashed #adadad;
}
.controls {
  display: flex;
  flex-direction: row;
  column-gap: 16px;
  padding: 0;
  justify-content: center;
  margin: 1rem;
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
  transition: all 60ms linear;

  &:hover {
    background-color: #333333;
    color: #fff;
  }
}
.btn--start {
  margin-top: 3rem;
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

.hide-this,
.hidden {
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

  &--deck-starter {
    cursor: pointer;

    h3 {
      font-size: 1rem;
      color: salmon;
      font-weight: bold;
    }

    &:hover {
      background-color: #ececec;
    }

  }
}</style>