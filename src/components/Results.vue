<template>
    <div class="results">
        <h5 v-for="c in secondDeck">{{ c.word }}</h5>
    </div>
</template>
<script>
export default {
    props: ["secondDeck"]
}
</script>
<style scoped>
    * {
        color: salmon;
    }
</style>