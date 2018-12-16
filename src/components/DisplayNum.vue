<template>
    <div class="display">
        <input type="number" min="0" max="99" class="result" v-model.number="score" v-on:input="$emit('score-change', score)"/>
    </div>
</template>


<script>
export default {
    name: 'DisplayNum',
    data: function () {
        return {
            score: 0
        }
    },
}
</script>

<style scoped>
    input.result {
        margin: 10px;
        height: 50px;
        width: 2em;
        font-size: 30px;
        text-align: center;
        font-weight: bolder;
        border: 2px solid #2c3e50;
        border-radius: 5px;
        background-color: rgba(44, 62, 80, 0.5);
        transition: background-color 50ms ease-out;
    }

    input.result:focus {
        background-color:  #ffffff;
        transition: background-color 300ms linear;
    }
</style>
