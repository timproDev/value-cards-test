<template>
  <div class="main">
    <button class="reset" @click.prevent="resetDeck">reset</button>
    <p class="number" :cards="cards" :cardsViewed="cardsViewed">Showing {{ cardsViewed + 1 }} of {{ cards.length }} cards</p>
    <Cards v-if="cardsViewed < cards.length" :cards="cards" :cardsViewed="cardsViewed" />
    <Results v-else :secondDeck="secondDeck" />
    <Controls :cards="cards"
      @card-removed="cardRemoved"
      @is-not-important="cardRemoved"
      @is-important="isImportant"
      @is-very-important="isVeryImportant"
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
  methods: {
    resetDeck() {
      this.cardsViewed = 0;
      this.cards.forEach((i) => {
        i.removed = false;        
      })
      console.log(this.cards)
    },
    isImportant() {
      this.importantDeck.push(this.cards[this.cardsViewed]);
      this.cardsViewed++;
    },
    isVeryImportant() {
      this.veryImportantDeck.push(this.cards[this.cardsViewed]);
      this.cardsViewed++;
      console.log("very important deck includes", this.veryImportantDeck)
    },
    cardPassed() {
      this.cards.push(this.cards.splice(this.cards.indexOf(this.cards[this.cardsViewed]), 1)[0]);
      console.log(this.cards)
    },
    cardRemoved() {
      this.cards[this.cardsViewed].removed = true
      this.cardsViewed++;
      console.log(this.cards)
    }
  },
  data() {
    return {
      cardsViewed: 0, // keep track of cards,
      importantDeck: [],
      veryImportantDeck: [],
      secondDeck: [],
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
          word: 'Adaptability',
          removed: false
        },
        {
          word: 'Adventure',
          removed: false
        },
        {
          word: 'Altruism',
          removed: false
        },
        {
          word: 'Ambition',
          removed: false
        },
        {
          word: 'Authenticity',
          removed: false
        },
        {
          word: 'Balance',
          removed: false
        },
        {
          word: 'Beauty',
          removed: false
        },
        {
          word: 'Being the best',
          removed: false
        },
        {
          word: 'Belonging',
          removed: false
        },
        {
          word: 'Career',
          removed: false
        },
        {
          word: 'Caring',
          removed: false
        },
        {
          word: 'Collaboration',
          removed: false
        },
        {
          word: 'Commitment',
          removed: false
        },
        {
          word: 'Community',
          removed: false
        },
        {
          word: 'Competence',
          removed: false
        },
        {
          word: 'Confidence',
          removed: false
        },
        {
          word: 'Connection',
          removed: false
        },
        {
          word: 'Contentment',
          removed: false
        },
        {
          word: 'Contribution',
          removed: false
        },
        {
          word: 'Cooperation',
          removed: false
        },
        {
          word: 'Courage',
          removed: false
        },
        {
          word: 'Creativity',
          removed: false
        },
        {
          word: 'Curiosity',
          removed: false
        },
        {
          word: 'Dignity',
          removed: false
        },
        {
          word: 'Diversity',
          removed: false
        },
        {
          word: 'Environment',
          removed: false
        },
        {
          word: 'Efficiency',
          removed: false
        },
        {
          word: 'Equality',
          removed: false
        },
        {
          word: 'Ethics',
          removed: false
        },
        {
          word: 'Excellence',
          removed: false
        },
        {
          word: 'Fairness',
          removed: false
        },
        {
          word: 'Faith',
          removed: false
        },
        {
          word: 'Family',
          removed: false
        },
        {
          word: 'Financial stability',
          removed: false
        },
        {
          word: 'Forgiveness',
          removed: false
        },
        {
          word: 'Freedom',
          removed: false
        },
        {
          word: 'Friendship',
          removed: false
        },
        {
          word: 'Fun',
          removed: false
        },
        {
          word: 'Future generations',
          removed: false
        },
        {
          word: 'Generosity',
          removed: false
        },
        {
          word: 'Giving back',
          removed: false
        },
        {
          word: 'Grace',
          removed: false
        },
        {
          word: 'Gratitude',
          removed: false
        },
        {
          word: 'Growth',
          removed: false
        },
        {
          word: 'Harmony',
          removed: false
        },
        {
          word: 'Health',
          removed: false
        },
        {
          word: 'Home',
          removed: false
        },
        {
          word: 'Honesty',
          removed: false
        },
        {
          word: 'Hope',
          removed: false
        },
        {
          word: 'Humility',
          removed: false
        },
        {
          word: 'Humor',
          removed: false
        },
        {
          word: 'Inclusion',
          removed: false
        },
        {
          word: 'Independence',
          removed: false
        },
        {
          word: 'Initiative',
          removed: false
        },
        {
          word: 'Integrity',
          removed: false
        },
        {
          word: 'Intuition',
          removed: false
        },
        {
          word: 'Job security',
          removed: false
        },
        {
          word: 'Joy',
          removed: false
        },
        {
          word: 'Justice',
          removed: false
        },
        {
          word: 'Kindness',
          removed: false
        },
        {
          word: 'Knowledge',
          removed: false
        },
        {
          word: 'Leadership',
          removed: false
        },
        {
          word: 'Learning',
          removed: false
        },
        {
          word: 'Legacy',
          removed: false
        },
        {
          word: 'Leisure',
          removed: false
        },
        {
          word: 'Love',
          removed: false
        },
        {
          word: 'Loyalty',
          removed: false
        },
        {
          word: 'Making a difference',
          removed: false
        },
        {
          word: 'Nature',
          removed: false
        },
        {
          word: 'Openness',
          removed: false
        },
        {
          word: 'Optimism',
          removed: false
        },
        {
          word: 'Order',
          removed: false
        },
        {
          word: 'Parenting',
          removed: false
        },
        {
          word: 'Patience',
          removed: false
        },
        {
          word: 'Patriotism',
          removed: false
        },
        {
          word: 'Peace',
          removed: false
        },
        {
          word: 'Perseverance',
          removed: false
        },
        {
          word: 'Personal fulfillment',
          removed: false
        },
        {
          word: 'Power',
          removed: false
        },
        {
          word: 'Pride',
          removed: false
        },
        {
          word: 'Recognition',
          removed: false
        },
        {
          word: 'Reliability',
          removed: false
        },
        {
          word: 'Resourcefulness',
          removed: false
        },
        {
          word: 'Respect',
          removed: false
        },
        {
          word: 'Responsibility',
          removed: false
        },
        {
          word: 'Risk-taking',
          removed: false
        },
        {
          word: 'Safety',
          removed: false
        },
        {
          word: 'Security',
          removed: false
        },
        {
          word: 'Self-discipline',
          removed: false
        },
        {
          word: 'Self-expression',
          removed: false
        },
        {
          word: 'Self-respect',
          removed: false
        },
        {
          word: 'Serenity',
          removed: false
        },
        {
          word: 'Service',
          removed: false
        },
        {
          word: 'Simplicity',
          removed: false
        },
        {
          word: 'Spirituality',
          removed: false
        },
        {
          word: 'Sportsmanship',
          removed: false
        },
        {
          word: 'Stewardship',
          removed: false
        },
        {
          word: 'Success',
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
          word: 'Tradition',
          removed: false
        },
        {
          word: 'Travel',
          removed: false
        },
        {
          word: 'Trust',
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
<style>
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
</style>