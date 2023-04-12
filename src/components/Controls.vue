<template>
    <div class="stage-1-buttons controls" v-if="stage == 1">
        <button type="button" class="remove" @click.prevent=isNotImportant>Not important</button>
        <button type="button" class="add" @click.prevent=isImportant>Important</button>
        <button type="button" class="pass" @click.prevent=passCard>Come back to</button>
    </div>
    <div class="stage-1-buttons controls" v-else-if="stage == 2">
        <span>Stage 2 buttons</span>
    </div>
</template>
<script>
export default {
    props: [
        "cards",
        "stage"
    ],
    emit: [
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
