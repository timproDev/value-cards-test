<template>
    <div class="cnt-block cnt-block--results">
        <h2>Your values are:</h2>
        <ul v-if="cards">
            <li v-for="c in cards">{{ c.word }}</li>
        </ul>
        <button
        type="button"
        class="btn btn--next-stage"
        @click.prevent="nextStage">
        Sort your values
        </button>
    </div>
</template>
<script>
export default {
    props: ["cards"],
    methods: {
        nextStage() {
            this.$emit('next-stage')
        }
    },
    emits: [
        'next-stage'
    ]
}
</script>