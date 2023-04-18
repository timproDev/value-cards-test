<template>
    <div class="cnt-block cnt-block--results">
        <h2>Your values are:</h2>
        <ul v-if="cards">
            <li v-for="c in cards">{{ c.word }}</li>
        </ul>
        <button
        type="button" 
            class="btn btn--reset"
            @click.prevent="resetDeck"
        >Restart</button>
    </div>
</template>
<script>
export default {
    props: ["cards"],
    methods: {
        resetDeck() {
            this.$emit('reset-deck')
        }
    },
    emit: [
        'reset-deck'
    ]
}
</script>