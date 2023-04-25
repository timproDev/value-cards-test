<template>
    <div class="controls-wrapper" v-show="!deckComplete">
        <!-- Section heading for control buttons -->
        <h4>How important?</h4>
        
        <!-- Control buttons for first round -->
        <div class="controls" v-if="deckRound == 1">
            <button type="button" class="btn btn--remove" @click.prevent=isNotImportant>Not important</button>
            <button type="button" class="btn btn--add" @click.prevent=isImportant>Important</button>
            <button type="button" class="btn btn--pass" @click.prevent=passCard>Pass</button>
        </div>
        
        <!-- Control buttons for second round -->
        <div class="controls" v-else-if="deckRound == 2">
            <button type="button" class="btn btn--remove" @click.prevent=isNotImportant>Little</button>
            <button type="button" class="btn btn--remove" @click.prevent=isNotImportant>Somewhat</button>
            <button type="button" class="btn btn--add" @click.prevent=isImportant>Very</button>
            <button type="button" class="btn btn--pass" @click.prevent=passCard>Pass</button>
        </div>
        
        <!-- Control buttons for third round -->
        <div class="controls" v-else-if="deckRound == 3">
            <button type="button" class="btn btn--remove" @click.prevent=isNotImportant>Moderately</button>
            <button type="button" class="btn btn--add" @click.prevent=isImportant>Super</button>
            <button type="button" class="btn btn--pass" @click.prevent=passCard>Pass</button>
        </div>
    </div>    
</template>

<script>

export default {
    // Receive props from parent component
    props: [
        'deckRound',
        'deckComplete'
    ],
    // Emit events to parent component
    emits: [
        "is-not-important",
        "is-important",
        "card-passed"
    ],
    methods: {
        // Emit event when "Not important" button is clicked
        isNotImportant() {
            this.$emit('is-not-important');
        },
        // Emit event when "Important" or "Very" button is clicked
        isImportant() {
            this.$emit('is-important');
        },
        // Emit event when "Pass" button is clicked
        passCard() {
            this.$emit('card-passed');
        }
    }
}
</script>