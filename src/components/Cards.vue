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
<style scoped>
    .card {
        border-radius: 8px;
        color: #fff;
        border: 1px solid #fff;
        display: flex;
        flex-direction: column;
        align-items: center;
        min-height: 400px;
    }
</style>