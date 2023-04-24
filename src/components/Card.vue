<template>
    <div class="card" :key="oneCard.word" ref="cardRef">
        <h3>{{ oneCard.word }}</h3>
    </div>
</template>
<script>

export default {
    props: [
        "cards"
    ]
}
</script>