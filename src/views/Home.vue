<template lang="">
    <div>
        <div class="cnt-block cnt-block--home-hero">
            <h2>About the exercise</h2>
            <p>In this exercise, you will be presented with 64 values, each of which you will determine its importance to you. There will be 3 rounds in order to filter the values down to your most important values.</p>
            <button type=button @click.prevent=startRoundOne class="btn btn--start">Start</button>
        </div>                
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