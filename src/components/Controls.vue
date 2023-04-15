<template>
    <div class="controls">
        <button type="button" class="remove" @click.prevent=isNotImportant>Not important</button>
        <button type="button" class="add" @click.prevent=isImportant>Important</button>
        <button type="button" class="pass" @click.prevent=passCard>Come back to</button>
    </div>
</template>
<script>
export default {
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
