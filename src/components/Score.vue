<template>
    <div class="score">
        <div class="score-inputs">
            <DisplayNum :score="value" />:
            <DisplayNum :score="value" />
        </div>
    </div>
</template>


<script>
import DisplayNum from './DisplayNum.vue'

export default {
    name: 'Score',
    components: {
        DisplayNum,
    },
    props: {
        value: Number,
    }
}
</script>

<style scoped>
.score {
    width: 80vw;
    margin-left: 10%;
    font-size: 2.5em;
    font-weight: bold;
    /* width: 80vw; */
}

.score-inputs {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
}
</style>
