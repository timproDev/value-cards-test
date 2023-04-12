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
      v-else :importantDeck="importantDeck" />

    <Controls
      :cards="cards"
      :cardsViewed="cardsViewed"
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
  watch: {
    // watch the number of cards view and increment stage value
    // cardsViewed(val) {
    //   if (val == cards.length) {
    //     stage++;
    //   }
    // }
  },
  methods: {
    resetDeck() {
      this.cardsViewed = 0;
      this.cards.forEach((i) => {
        i.removed = false;        
      })
    },
    isImportant() {
      this.importantDeck.push(this.cards[this.cardsViewed]);
      this.cardsViewed++;
    },
    cardPassed() {
      this.cards.push(this.cards.splice(this.cards.indexOf(this.cards[this.cardsViewed]), 1)[0]);
    },
    cardRemoved() {
      this.cards[this.cardsViewed].removed = true; // may not need this property
      this.cardsViewed++;
    },
    goToNext() {
      this.stage++;
    }
  },
  data() {
    return {
      cardsViewed: 0, // keep track of cards,
      stage:1,
      importantDeck: [],
      cards: [
        {
          word: 'Accountability',
          removed: false
        },
        {
          word: 'Achievement',
          removed: false
        },
        {
          word: 'Teamwork',
          removed: false
        },
        {
          word: 'Thrift',
          removed: false
        },
        {
          word: 'Time',
          removed: false
        },
        {
          word: 'Truth',
          removed: false
        },
        {
          word: 'Understanding',
          removed: false
        },
        {
          word: 'Uniqueness',
          removed: false
        },
        {
          word: 'Usefulness',
          removed: false
        },
        {
          word: 'Vision',
          removed: false
        },
        {
          word: 'Vulnerability',
          removed: false
        },
        {
          word: 'Wealth',
          removed: false
        },
        {
          word: 'Well-being',
          removed: false
        },
        {
          word: 'Wholeheartedness',
          removed: false
        },
        {
          word: 'Wisdom',
          removed: false
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