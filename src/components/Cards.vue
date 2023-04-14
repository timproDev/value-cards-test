<template>
    <div class="card"
        v-for="(card, ci) in cards"
        :key="card.word"
        v-show="cardsViewed === ci"
    >
      <h3>{{ card.word }}</h3>
      <p v-if="card.definition">{{ card.definition }}</p>
    </div>
</template>
<script>
export default {
    props: [
        "cards",
        "cardsViewed"
    ]
}
</script>