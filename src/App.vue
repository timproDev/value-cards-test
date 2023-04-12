<template>
  <div class="main">
    
    <button
      type="button" 
      class="reset"
      @click.prevent="resetDeck"
    >reset</button>
    
    <p
      :class="cardsViewed < cards.length ? `show-this` : `hide-this`"
      class="number"
      :cards="cards"
      :cardsViewed="cardsViewed"
    >{{ (cards.length - cardsViewed) }} cards remaining</p>
    
    <button
      type="button"
      class="next-btn"
      v-if="cardsViewed == cards.length"
      :cards="cards"
      :cardsViewed="cardsViewed"
      @click.prevent="goToNext"
    >Go to next stage</button>

    <Cards
      v-if="cardsViewed < cards.length"
      :cards="cards"
      :cardsViewed="cardsViewed" />

    <Results
      v-if="cardsViewed == cards.length" :cards="cards" />

    <Controls
      :play="play"
      :stage="stage"
      @is-not-important="cardRemoved"
      @is-important="isImportant"
      @card-passed="cardPassed"
      />

  </div>
</template>
<script>
import Cards from './components/Cards.vue';
import Controls from './components/Controls.vue';
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: {
    Cards,
    Controls,
    Results
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
      this.cards.forEach((i) => {
        i.important = false;        
      })
    },
    isImportant() {
      // this.importantDeck.push(this.cards[this.cardsViewed]); // approach to add to new deck
      this.cards[this.cardsViewed].important = true;
      this.cardsViewed++;
    },
    cardPassed() {
      this.cards.push(this.cards.splice(this.cards.indexOf(this.cards[this.cardsViewed]), 1)[0]);
    },
    cardRemoved() {
      this.cardsViewed++;
    },
    goToNext() {
      this.stage++;
    }
  },
  data() {
    return {
      cardsViewed: 0, // keep track of cards
      play: true,
      stage: 1,
      cards: [
        {
          word: 'Accountability',
          important: false
        },
        {
          word: 'Achievement',
          important: false
        },
        {
          word: 'Teamwork',
          important: false
        },
        {
          word: 'Thrift',
          important: false
        },
        {
          word: 'Time',
          important: false
        }
      ]
    }    
  }
}
</script>
<style lang="scss">
body {
  background-color: rgb(45, 45, 45);
}
.main {
  width: 500px;
  margin: 0 auto;
}
p.number {
  color:aqua;
}
.controls {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    row-gap: 32px;
    padding-top: 32px;
}
button {
    background-color: grey;
    border: 1px solid black;
    outline: none;
    width: 60px;
    height: 60px;
    cursor: pointer;
    &:hover {
        background-color: #fff
    }
}
.hide-this {
  visibility: hidden;
  opacity: 0;
}
</style>