<template>
  <div class="main">
    <div class="cnt-block cnt-block--home-header">
      <h1>Value Cards</h1>
      <p>The Common Core Values Exercise</p>
    </div>

    <Transition appear mode="out-in">
      <Home v-if="stage == 1" @next-stage="nextStage" />
      <DeckPlay v-else-if="stage == 2" :cards="cards" @next-stage="nextStage" @go-back="goBack" />
    </Transition>

  </div>
</template>
<script>
import Home from './views/Home.vue'
import DeckPlay from './views/DeckPlay.vue'

export default {
  name: 'App',
  components: {
    Home,
    DeckPlay
  },
  methods: {
    nextStage() {
      this.stage++;
    },
    goBack() {
      this.stage = 1;
    }
  },
  data() {
    return {
      stage: 1,
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
        // { word: 'Challenge' },
        // { word: 'Belief' },
        // { word: 'Nurture' },
        // { word: 'Hope' },
        // { word: 'Gratitude' },
        // { word: 'Self-Expression' },
        // { word: 'Sacredness' },
        // { word: 'Calm' },
        // { word: 'Change' },
        // { word: 'Learning' },
        // { word: 'Accomplishment' },
        // { word: 'Nature' },
        { word: 'Community' },
        // { word: 'Fairness' },
        // { word: 'Partnership' },
        // { word: 'Faithfulness' },
        // { word: 'Adventure' },
        // { word: 'Contribution' },
        // { word: 'Truth' },
        // { word: 'Pleasure' },
        // { word: 'Security' },
        // { word: 'Service' },
        // { word: 'Happiness' },
        // { word: 'Power' },
        // { word: 'Serenity' },
        // { word: 'Enlightenment' },
        // { word: 'Play' },
        // { word: 'Relationship' },
        { word: 'Inner Strength' },
        // { word: 'Invention' },
        // { word: 'Encouragement' },
        // { word: 'Fun' },
        // { word: 'Equanimity' },
        // { word: 'Reliability' },
        // { word: 'Honor' },
        // { word: 'Work' },
        // { word: 'Order' },
        // { word: 'Connection' },
        // { word: 'Structure' },
        // { word: 'Strength' },
        // { word: 'Intellect' },
        // { word: 'Spirituality' },
        // { word: 'Passion' },
        // { word: 'Self-Respect' },
        // { word: 'Imagination' },
        // { word: 'Planning' },
        // { word: 'Humor' },
        // { word: 'Patience' },
        // { word: 'Friendship' },
        // { word: 'Joy' },
        // { word: 'Honesty' },
        // { word: 'Wholeness' },
        // { word: 'Persuasion' },
        // { word: 'Intuition' },
        // { word: 'Rules' },
        // { word: 'Dignity' },
        // { word: 'Family' },
        // { word: 'Love' },
        { word: 'Home' },
        { word: 'Leadership' },
        { word: 'Dependability' },
        { word: 'Consistency' },
        // { word: 'Grace' },
        // { word: 'Mastery' },
        // { word: 'Laughter' },
        // { word: 'Integrity' },
        // { word: 'Support' },
        // { word: 'Winning' },
        // { word: 'Growth' },
        // { word: 'Creativity' },
        // { word: 'Loyalty' },
        // { word: 'Health' },
        // { word: 'Tradition' },
        // { word: 'Compassion' },
        // { word: 'Sexuality' },
        // { word: 'Respect' },
        // { word: 'Safety' },
        // { word: 'Attention' },
        // { word: 'Spontaneity' },
        // { word: 'Courage' },
        // { word: 'Understanding' },
        // { word: 'Pride' },
        // { word: 'Rituals' },
        // { word: 'Wealth' },
        // { word: 'Sensuality' },
        // { word: 'Justice' },
        // { word: 'Trust' },
        // { word: 'Discovery' },
        // { word: 'Vitality' },
        // { word: 'Feelings' },
        // { word: 'Self-Control' },
        // { word: 'Freedom' },
        { word: 'Kindness' },
        { word: 'Independence' },
        { word: 'Openness' }

      ],
      importantDeck: []
    }
  }
}
</script>