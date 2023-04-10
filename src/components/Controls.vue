<template>
    <div class="controls">
      <button type="button" class="remove" @click.prevent=removeCard>remove</button>
      <button type="button" class="add" @click.prevent=selectCard>keep</button>
      <button type="button" class="pass" @click.prevent=passCard>pass</button>
    </div>
</template>
<script>
export default {
    props: [
        "cards"
    ],
    emit: [
        "card-selected",
        "card-removed",
        "card-passed"
    ],
    methods: {
        selectCard() {
            this.$emit('card-selected');
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