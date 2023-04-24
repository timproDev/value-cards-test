<template>
    <Transition mode="out-in" name="sli" type="transition">
        <div class="card" :key="cards.word">
            <h3>{{ cards.word }}</h3>
        </div>
    </Transition>
</template>
<script>

export default {
    props: [
        "cards"
    ]
}
</script>