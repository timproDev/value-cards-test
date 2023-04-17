<template>
    <div class="controls-wrapper">
        <h4>How important?</h4>
        <div class="controls" v-if="deckRound == 1">
            <button type="button" class="remove" @click.prevent=isNotImportant>Not important</button>
            <button type="button" class="add" @click.prevent=isImportant>Important</button>
            <button type="button" class="pass" @click.prevent=passCard>Come back to</button>
        </div>
        <div class="controls" v-else-if="deckRound == 2">
            <button type="button" class="remove" @click.prevent=isNotImportant>Little</button>
            <button type="button" class="remove" @click.prevent=isNotImportant>Somewhat</button>
            <button type="button" class="add" @click.prevent=isImportant>Very</button>
            <button type="button" class="pass" @click.prevent=passCard>Come back to</button>
        </div>
        <div class="controls" v-else-if="deckRound == 3">
            <button type="button" class="remove" @click.prevent=isNotImportant>Moderately</button>
            <button type="button" class="add" @click.prevent=isImportant>Super</button>
            <button type="button" class="pass" @click.prevent=passCard>Come back to</button>
        </div>
    </div>    
</template>
<script>
export default {
    props: [
        'deckRound'
    ],
    emits: [
        "is-not-important",
        "is-important",
        "card-passed"
    ],
    methods: {
        isNotImportant() {
            this.$emit('is-not-important')
        },
        isImportant() {
            this.$emit('is-important')
        },
        passCard() {
            this.$emit('card-passed');
        }
    }
}
</script>
