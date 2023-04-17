<template lang="">
    <button
      type="button"
      class="btn btn--next"
      v-if="cardsViewed == cards.length"      
      @click.prevent="goToNext"
    >
    <slot>
        Go to next
    </slot>
    </button>
</template>
<script>
export default {
    props: [
        "cards",
        "cardsViewed"
    ],
    methods: {
        goToNext() {
            this.$emit('go-to-next')
        }
    },
    emit: [
        'go-to-next'
    ]
}
</script>
<style lang="">
    
</style>