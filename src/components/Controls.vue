<template>
    <div class="controls">
      <button type="button" class="remove" @click.prevent=isNotImportant>Not important</button>
      <button type="button" class="add" @click.prevent=isImportant>Important</button>
      <button type="button" class="add" @click.prevent=isVeryImportant>Very important</button>
      <button type="button" class="pass" @click.prevent=passCard>Come back to</button>
    </div>
</template>
<script>
export default {
    props: [
        "cards"
    ],
    emit: [
        "card-removed",
        "is-not-important",
        "is-important",
        "is-very-important",
        "card-passed"
    ],
    methods: {
        isNotImportant() {
            this.$emit('is-not-important')
        },
        isImportant() {
            this.$emit('is-important')
        },
        isVeryImportant() {
            this.$emit('is-very-important')
        },
        removeCard() {
            this.$emit('card-removed');
        },
        passCard() {
            this.$emit('card-passed');
        }
    }
}
</script>
<style lang="scss">
    .controls {
        display: flex;
        flex-direction: row;
        justify-content: space-evenly;
        row-gap: 32px;
        padding-top: 32px;
    }
    button {
        background-color: grey;
        border: 1px solid black;
        outline: none;
        width: 60px;
        height: 60px;
        cursor: pointer;
        &:hover {
            background-color: #fff
        }
    }
</style>