<template lang="">
    <button
      type="button"
      class="btn btn--next"
      @click.prevent="goToNext"
    >
    <slot>
        Go to next
    </slot>
    </button>
</template>
<script>
export default {
    methods: {
        goToNext() {
            this.$emit('go-to-next')
        }
    },
    emits: [
        'go-to-next'
    ]
}
</script>
<style lang="">
    
</style>