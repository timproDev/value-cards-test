<template>
    <div class="controls-wrapper" v-show="!deckComplete">
        <!-- Section heading for control buttons -->
        <h4>How important?</h4>

        <!-- Control buttons for first round -->
        <div class="controls" v-if="deckRound == 1">
            <div class="btn-group">
                <button type="button" class="btn btn--remove" @click.prevent=isNotImportant></button>
                <label>Not important</label>
            </div>
            <div class="btn-group">
                <button type="button" class="btn btn--add" @click.prevent=isImportant></button>
                <label>Important</label>
            </div>
            <div class="btn-group btn-group--pass">
                <button type="button" class="btn btn--pass" @click.prevent=passCard></button>
                <label>Pass</label>
            </div>
        </div>

        <!-- Control buttons for second round -->
        <div class="controls" v-else-if="deckRound == 2">
            <div class="btn-group">
                <button type="button" class="btn btn--remove" @click.prevent=isNotImportant></button>
                <label>Little</label>
            </div>
            <div class="btn-group">
                <button type="button" class="btn btn--remove" @click.prevent=isNotImportant></button>
                <label>Somewhat</label>
            </div>
            <div class="btn-group">
                <button type="button" class="btn btn--add" @click.prevent=isImportant></button>
                <label>Very</label>
            </div>
            <div class="btn-group btn-group--pass">
                <button type="button" class="btn btn--pass" @click.prevent=passCard></button>
                <label>Pass</label>
            </div>
        </div>

        <!-- Control buttons for third round -->
        <div class="controls" v-else-if="deckRound == 3">
            <div class="btn-group">
                <button type="button" class="btn btn--remove" @click.prevent=isNotImportant></button>
                <label>Moderately</label>
            </div>
            <div class="btn-group">
                <button type="button" class="btn btn--add" @click.prevent=isImportant></button>
                <label>Super</label>
            </div>
            <div class="btn-group btn-group--pass">
                <button type="button" class="btn btn--pass" @click.prevent=passCard></button>
                <label>Pass</label>
            </div>
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