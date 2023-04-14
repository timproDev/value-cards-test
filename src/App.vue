<template>
  <div class="main">
    
    <CardCounter
      :cards="cards"
      :cardsViewed="cardsViewed"
    />    
    
    <NextButton
        :cards="cards"
        :cardsViewed="cardsViewed"
        @go-to-next="goToNext"
      />    

    <Cards
      v-if="cardsViewed < cards.length"
      :cards="cards"
      :cardsViewed="cardsViewed" />

    <Results
      v-if="cardsViewed == cards.length" :importantDeck="importantDeck" />

    <Controls
      v-show="play == true"
      @is-not-important="isNotImportant"
      @is-important="isImportant"
      @card-passed="cardPassed"
      />      

      <button
        type="button" 
        class="btn btn--reset"
        @click.prevent="resetDeck"
      >reset</button>
      
  </div>
</template>
<script>
import Cards from './components/Cards.vue';
import Controls from './components/Controls.vue';
import Results from './components/Results.vue'
import CardCounter from './components/CardCounter.vue'
import NextButton from './components/NextButton.vue'

export default {
  name: 'App',
  components: {
    Cards,
    NextButton,
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
  background-color: rgb(112, 112, 112);
}
.main {
  width: 400px;
  margin: 0 auto;
}
p.number {
  color:aqua;
}
.controls {
    display: flex;
    flex-direction: row;
    column-gap: 8px;
    padding-top: 24px;
    justify-content: center;    
}
button, .btn {
  position: relative;
  display: inline-flex;
  text-decoration: none;
  flex-grow: 1;
  align-items: center;
  justify-content: center;
  transition: all 100ms linear;
  //
    background-color: aqua;
    border: none;
    outline: none;
    height: 120px;
    cursor: pointer;
    border-radius: 160px;
    width: 80px;
    height: 80px;

    &:hover {
        background-color: #fff;
    }
    &--reset {
      background-color: #202020;
      border: none;
      color: white;
      text-decoration: underline;
      display: inline;
      height: auto;
      text-align: center;
      width: 100%;
      margin-top: 24px;
      padding: 1rem;
      &:hover {
        color: #000;
      }
    }
}
.hide-this {
  visibility: hidden;
  opacity: 0;
}

.card {
        border-radius: 8px;
        background-color: #262e35;
        color: #fff;
        border: 1px solid #181b1d;
        display: flex;
        flex-direction: column;
        align-items: center;
        min-height: 600px;
        justify-content: center;
        align-content: center;
        box-shadow:
            0px 2.8px 2.2px rgba(0, 0, 0, 0.02),
            0px 6.7px 5.3px rgba(0, 0, 0, 0.028),
            0px 12.5px 10px rgba(0, 0, 0, 0.035),
            0px 22.3px 17.9px rgba(0, 0, 0, 0.042),
            0px 41.8px 33.4px rgba(0, 0, 0, 0.05),
            0px 100px 80px rgba(0, 0, 0, 0.07)
            ;
    }
</style>