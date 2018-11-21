<template>
    <div class="competitors">
        <div class="inputs-row">
            <DisplayText  v-model="nameHome" v-on:team-change="updateTeam(1, $event)"/>:
            <DisplayText  v-model="nameAway" v-on:team-change="updateTeam(2, $event)"/>
        </div>
        <div class="inputs-row">
            <DisplayNum v-model="scoreHome"  v-on:score-change="updateScore(1, $event)"/>:
            <DisplayNum v-model="scoreHome"  v-on:score-change="updateScore(2, $event)"/>
        </div>
        <div class="control-area">
            <button v-on:click="send_request()">Update</button>
        </div>
    </div>
</template>


<script>
import DisplayNum from './DisplayNum.vue'
import DisplayText from './DisplayText.vue'

export default {
    name: 'Competitors',
    components: {
        DisplayText,
        DisplayNum,
    },
    data: function () {
        return {
            nameHome: "Heim",
            nameAway: "Gast",
            scoreHome: 0,
            scoreAway: 0
        }
    },
    methods: {
        updateTeam(HoA, val) {
            if (HoA == 1) {
                this.nameHome = val;
            } else {
                this.nameAway = val;
            }
        },
        updateScore(HoA, val) {
            if (HoA == 1) {
                this.scoreHome = val;
            } else {
                this.scoreAway = val;
            }
        },
        send_request() {
            var msg = this.nameHome + ', ' + this.nameAway;
            console.log(msg);
        }
    },
}


</script>

<style scoped>
.competitors {
    width: 80vw;
    margin-left: 10%;
    font-size: 2.5em;
    font-weight: bold;
}

.inputs-row {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
}

.control-area {
    margin-top: 2vh;
}

</style>
