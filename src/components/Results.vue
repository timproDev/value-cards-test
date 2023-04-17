<template>
    <div class="results">
        <h2>Congratulations on completing round one</h2>
        <p>The values you have chosen are:</p>
        <h3 v-for="c in cards">{{ c.word }}</h3>
    
    </div>
</template>
<script>
export default {
    props: ["cards"]
}
</script>