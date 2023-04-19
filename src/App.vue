<template>
  <div class="main">
    <div class="cnt-block cnt-block--home-header">
      <h1>Value Cards</h1>
      <p>The Common Core Values Exercise</p>
    </div>

    <Transition appear mode="out-in">

      <Home v-if="deckRound == 0" @start-round="roundUp" />

      <RoundOne v-else-if="deckRound == 1" :deckRound="deckRound" :cards="cards" @round-finished="roundUp"
        @push-to-round-one="pushOne" />

      <RoundTwo v-else-if="deckRound == 2" :deckRound="deckRound" :cards="roundOneImportant" @round-finished="roundUp"
        @push-to-round-two="pushTwo" />

      <RoundThree v-else-if="deckRound == 3" :deckRound="deckRound" :cards="roundTwoImportant" @round-finished="roundUp"
        @push-to-round-three="pushThree" />

      <Results v-else :cards="roundThreeImportant" @reset-deck="resetDeck" />

    </Transition>

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
        { word: 'Beauty' },
        { word: 'Peace' },
        { word: 'Control' },
        { word: 'Challenge' },
        { word: 'Belief' },
        { word: 'Nurture' },
        { word: 'Hope' },
        { word: 'Gratitude' },
        { word: 'Self-Expression' },
        { word: 'Sacredness' },
        { word: 'Calm' },
        { word: 'Change' },
        { word: 'Learning' },
        { word: 'Accomplishment' },
        { word: 'Nature' },
        { word: 'Community' },
        { word: 'Fairness' },
        { word: 'Partnership' },
        { word: 'Faithfulness' },
        { word: 'Adventure' },
        { word: 'Contribution' },
        { word: 'Truth' },
        { word: 'Pleasure' },
        { word: 'Security' },
        { word: 'Service' },
        { word: 'Happiness' },
        { word: 'Power' },
        { word: 'Serenity' },
        { word: 'Enlightenment' },
        { word: 'Play' },
        { word: 'Relationship' },
        { word: 'Inner' },
        { word: 'Strength' },
        { word: 'Invention' },
        { word: 'Encouragement' },
        { word: 'Fun' },
        { word: 'Equanimity' },
        { word: 'Reliability' },
        { word: 'Honor' },
        { word: 'Work' },
        { word: 'Order' },
        { word: 'Connection' },
        { word: 'Structure' },
        { word: 'Strength' },
        { word: 'Intellect' },
        { word: 'Spirituality' },
        { word: 'Passion' },
        { word: 'Self-Respect' },
        { word: 'Imagination' },
        { word: 'Planning' },
        { word: 'Humor' },
        { word: 'Patience' },
        { word: 'Friendship' },
        { word: 'Joy' },
        { word: 'Honesty' },
        { word: 'Wholeness' },
        { word: 'Persuasion' },
        { word: 'Intuition' },
        { word: 'Rules' },
        { word: 'Dignity' },
        { word: 'Family' },
        { word: 'Love' },
        { word: 'Home' },
        { word: 'Leadership' },
        { word: 'Dependability' },
        { word: 'Consistency' },
        { word: 'Grace' },
        { word: 'Mastery' },
        { word: 'Laughter' },
        { word: 'Integrity' },
        { word: 'Support' },
        { word: 'Winning' },
        { word: 'Growth' },
        { word: 'Creativity' },
        { word: 'Loyalty' },
        { word: 'Health' },
        { word: 'Tradition' },
        { word: 'Compassion' },
        { word: 'Sexuality' },
        { word: 'Respect' },
        { word: 'Safety' },
        { word: 'Attention' },
        { word: 'Spontaneity' },
        { word: 'Courage' },
        { word: 'Understanding' },
        { word: 'Pride' },
        { word: 'Rituals' },
        { word: 'Wealth' },
        { word: 'Sensuality' },
        { word: 'Justice' },
        { word: 'Trust' },
        { word: 'Discovery' },
        { word: 'Vitality' },
        { word: 'Feelings' },
        { word: 'Self-Control' },
        { word: 'Freedom' },
        { word: 'Kindness' },
        { word: 'Independence' },
        { word: 'Openness' }
      ],
      roundOneImportant: [],
      roundTwoImportant: [],
      roundThreeImportant: []
    }
  }
}
</script>
<style lang="scss"></style>