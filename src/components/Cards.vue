<template>
        <div class="cards-wrapper">
            <Transition mode="out-in" name="sli">
                <div v-if="!deckComplete" class="card" :key="cards.word">
                    <h3>{{ cards.word }}</h3>
                </div>
            </Transition>
        </div>
</template>
<script>

export default {
    props: [
        "cards",
        "cardsViewed",
        "deckComplete"
    ]    
}
</script>