<template lang="">
    <div>
        <h1>Home</h1>
        <button type=button @click.prevent=startRoundOne>Start</button>
    </div>
</template>
<script>
export default {
    emits:[
        'start-round'
    ],
    methods: {
        startRoundOne() {
            this.$emit('start-round')
        }
    },
}
</script>
<style lang="">
    
</style>