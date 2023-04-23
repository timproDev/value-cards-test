<template>
        <div class="cards-wrapper">
            <Transition mode="out-in" name="sli">
                <div class="card" :key="cardsViewed">
                    <h3>{{ cards.word }}</h3>
                </div>
            </Transition>
        </div>
</template>
<script>

export default {
    props: [
        "cards",
        "cardsViewed"
    ]    
}
</script>