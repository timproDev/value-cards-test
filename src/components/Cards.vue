<template>
        <div class="cards-wrapper">
            <Transition mode="out-in" name="sli">
                <div class="card" :key="oneCard.word" ref="cardRef">
                    <h3>{{ oneCard.word }}</h3>
                </div>
            </Transition>
        </div>
</template>
<script>

export default {
    props: [
        "cards",
        "cardsViewed"
    ],
    computed: {
        oneCard() {
            return this.cards[this.cardsViewed];
        }
    }
}
</script>