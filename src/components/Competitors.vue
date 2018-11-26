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
            <button v-on:click="send_data_req()">Update</button><i class="spacing"/>
            <button v-on:click="send_time_req('start')">Start Timer</button><i class="spacing"/>
            <button v-on:click="send_get()">Stop Timer</button>
        </div>
    </div>
</template>


<script>
import DisplayNum from './DisplayNum.vue'
import DisplayText from './DisplayText.vue'
// var axios = require('axios')
// import * as http from "http";
// const httpModule = require("http");
// import VueResource from 'vue-resource';

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
            backend_url: '192.168.0.50:3000',
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
            } else {
                this.scoreAway = val;
            }
        },
        send_data_req() {
            // var msg = { 
            //     "home": this.nameHome,
            //     "away": this.nameAway,
            //     "scoreHome": this.scoreHome,
            //     "scoreAway": this.scoreAway,
            // };
            var msg = {"home": this.scoreHome, "away": this.scoreAway, "minutes": 0};
            var headers = { "Content-Type": "application/json",
                "Access-Control-Allow-Methods": "POST",
                "Access-Control-Allow-Origin": '*',
                "Access-Control-Allow-Headers": "Content-Type",
                // "X-PINGOTHER": "pingpong",
            };
            this.$http.post('http://'+this.backend_url+'/competitor', msg, headers).then(response => {
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
                var msg = {"time": 0,};
            } else if (variant == "stop") {
                msg = {"time": -1,};
            }
            var headers = { "Content-Type": "application/json" };
            this.$http.post('http://'+this.backend_url, msg, headers).then(response => {
                console.log('status: ' + response.status)
                var someData = response.body;
                console.log(someData);
            }, response => {
                console.log('status: ' + response.status);
                console.log('body: ' + response.body);
            });
        },
        send_get() {
            var headers = { "Content-Type": "text/plain" };
            this.$http.get('http://'+this.backend_url, headers).then(response => {
                console.log('status: ' + response.status)
                var someData = response.body;
                console.log(someData);
            }, response => {
                console.log('status: ' + response.status);
                console.log('body: ' + response.body);
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
