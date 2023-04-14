<template lang="">
    <p
    :class="cardsViewed < cards.length ? `show-this` : `hide-this`"
    class="number"
    >{{ (cards.length - cardsViewed) }} cards remaining</p>
</template>
<script>
export default {
    props: [
        "cards",
        "cardsViewed"
    ]
}
</script>
<style lang="">
    
</style>