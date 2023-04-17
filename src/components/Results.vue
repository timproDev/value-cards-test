<template>
    <div class="results">
        <h2>Your values are:</h2>
        <ul v-if="cards">
            <li v-for="c in cards">{{ c.word }}</li>
        </ul>
    
    </div>
</template>
<script>
export default {
    props: ["cards"]
}
</script>