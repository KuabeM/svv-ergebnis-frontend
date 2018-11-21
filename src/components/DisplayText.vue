<template>
    <div class="display">
        <input type="Text" class="result" v-model="teamName" v-on:input="$emit('team-change', teamName)"/>
    </div>
</template>


<script>
export default {
    name: 'DisplayText',
    data: function () {
        return {
            teamName: "Team Name"
        }
    },
}
</script>

<style scoped>
    input.result {
        margin: 10px;
        height: 50px;
        width: 35vw;
        font-size: 20px;
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
