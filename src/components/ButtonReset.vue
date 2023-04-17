<template lang="">
    <button
        type="button" 
        class="btn btn--reset"
        @click.prevent="resetDeck"
      >reset</button>
</template>
<script>
export default {
    methods: {
        resetDeck() {
            this.$emit('reset-deck')
        }
    },
    emit: [
        'reset-deck'
    ]
}
</script>
<style lang="">
    
</style>