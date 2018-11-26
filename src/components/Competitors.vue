<template>
    <div class="competitors">
        <div class="inputs-row">
            <DisplayNum v-model="minutes" v-on:score-change="updateScore(0, $event)" />
        </div>
        <div class="inputs-row">
            <DisplayText  v-model="nameHome" v-on:team-change="updateTeam(1, $event)"/>:
            <DisplayText  v-model="nameAway" v-on:team-change="updateTeam(2, $event)"/>
        </div>
        <div class="inputs-row">
            <DisplayNum v-model="scoreHome"  v-on:score-change="updateScore(1, $event)"/>:
            <DisplayNum v-model="scoreHome"  v-on:score-change="updateScore(2, $event)"/>
        </div>
        <div class="control-area">
            <button v-on:click="send_data_req()">Update</button><i class="spacing"/>
            <button v-on:click="send_time_req('start')">Start Timer</button><i class="spacing"/>
            <button v-on:click="send_time_req('set')">Set Timer</button><i class="spacing"/>
            <button v-on:click="send_time_req('stop')">Stop Timer</button>
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
            scoreAway: 0,
            minutes: 0,
            backend_url: '192.168.0.50:4000',
            postResult: []
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
            } else if (HoA == 2){
                this.scoreAway = val;
            } else if (HoA == 0){
                this.minutes = val;
            } else {
                console.log("bad option");
            }
        },
        send_data_req() {
            this.send_teams_req();
            this.send_score_req();
        },
        send_teams_req() {
            var msg = { 
                "name_home": this.nameHome,
                "name_away": this.nameAway,
            };
            var headers = { "Content-Type": "application/json",};
            this.$http.post('http://'+this.backend_url+'/teams', msg, headers).then(response => {
                console.log('status: ' + response.status)
                var someData = response.body;
                console.log(someData);
            }, response => {
                console.log('status: ' + response.status);
                console.log('body: ' + response);
            });
        },
        send_score_req() {
            var msg = { 
                "score_home": this.scoreHome,
                "score_away": this.scoreAway,
            };
            var headers = { "Content-Type": "application/json",};
            this.$http.post('http://'+this.backend_url+'/score', msg, headers).then(response => {
                console.log('status: ' + response.status)
                var someData = response.body;
                console.log(someData);
            }, response => {
                console.log('status: ' + response.status);
                console.log('body: ' + response);
            });
        },
        send_time_req(variant) {
            if (variant == "start") {
                var msg = {"min": 254,};
            } else if (variant == "stop") {
                msg = {"min": 255,};
            } else if (variant == "set") {
                msg = {"min": this.minutes,};
            }
            var headers = { "Content-Type": "application/json" };
            this.$http.post('http://'+this.backend_url+'/minutes', msg, headers).then(response => {
                console.log('status: ' + response.status)
                var someData = response.body;
                console.log(someData);
            }, response => {
                console.log('status: ' + response.status);
                console.log('body: ' + response.body);
            });
        },
        send_get() {
            var headers = { "Content-Type": "application/json",};
            this.$http.get('http://'+this.backend_url+'/', headers).then(response => {
                console.log('status: ' + response.status)
                var someData = response.body;
                console.log(someData);
            }, response => {
                console.log('status: ' + response.status);
                console.log('body: ' + response);
            });
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

.spacing {
    margin-left: 1vh;
}

</style>
