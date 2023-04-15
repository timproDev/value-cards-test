<template>
    <div class="results">
        <p>The values you have chosen are:</p>
        <h3 v-for="c in roundOneImportant">{{ c.word }}</h3>
    
    </div>
</template>
<script>
export default {
    props: ["roundOneImportant"]
}
</script>
<style scoped>
    * {
        color: #fff;
    }
</style>