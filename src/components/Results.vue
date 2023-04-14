<template>
    <div class="results">
        <p>The values you have chosen are:</p>
        <h3 v-for="c in importantDeck">{{ c.word }}</h3>
    
    </div>
</template>
<script>
export default {
    props: ["importantDeck"],
    // computed: {
    //     returnImportant() {
    //         return this.cards.filter(function(c){
    //             return c.important;
    //         })
    //     }
    // }
}
</script>
<style scoped>
    * {
        color: #fff;
    }
</style>