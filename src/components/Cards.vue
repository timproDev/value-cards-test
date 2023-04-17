<template>
    <Transition mode="out-in">
        <div class="cards-wrapper" v-if="this.deckStarted == false">
            <div class="card card--deck-starter" @click="startDeck">
                <h3>Tap to start deck</h3>
            </div>
        </div>    
        <div class="cards-wrapper" v-else-if="this.deckStarted == true">
            <div class="card"
                v-for="(card, ci) in cards"
                :key="card.word"
                v-show="cardsViewed === ci"
            >
            <h3>{{ card.word }}</h3>
            <p v-if="card.definition">{{ card.definition }}</p>
            </div>
        </div>
    </Transition>
</template>
<script>

export default {
    props: [
        "cards",
        "cardsViewed",
        "deckStarted"
    ],
    emits: ['start-deck'],
    methods: {
        startDeck() {
            this.$emit('start-deck');      
        }
    }
}
</script>